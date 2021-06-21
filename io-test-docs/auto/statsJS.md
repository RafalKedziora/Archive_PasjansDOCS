# Statystyki globalne

>Testy wykonali: Paulina Gayny oraz Damian Bugaj

System potrafi liczyć statystki gracza, chodzi głównie o liczbie wygranych, remisów oraz przegranych. 
Testy, jakie wykonaliśmy dla komponentu statystyk, obejmowały renderowanie danych, które przychodzą z API, 
dlatego też zdecydowaliśmy się na mockowanie danych z API. 
Dzięki temu nie martwiliśmy się tym czy API działa i czy przypadkiem model danych się nie zmienił.
Jedyne, na czym się skupiliśmy to testowanie renderowania komponentu.

```javascript
test('it renders data from API', async () => {
    jest.mock("axios");
    axios.get = jest.fn();
    let mock = {
        ID: 1,
        Avatar: 'https://i.pinimg.com/736x/3b/37/cd/3b37cd80d4f092ed392b1453b64cf0d0.jpg',
        Nazwa: "Testowy Kot",
        Ranking: 1,
        Wygrane: 999,
        Remisy: 0,
        Przegrane: 0
    };

    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: [mock]
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    const listItem = container.querySelector('#stats-table tr:first-child');
    const statistic = listItem.querySelector('td:last-child');

    expect(listItem).not.toBeNull();
    expect(statistic.innerHTML).toBe(`${mock.Wygrane}/${mock.Remisy}/${mock.Przegrane}`);
});
```

Statystyki mogą być filtrowane, więc przetestowaliśmy to:
```javascript
test('can filter by top 10', async () => {
    jest.mock("axios");
    axios.get = jest.fn();
    
    let mock = [
        {
            ID: 1,
            Ranking: 4,
        },
        {
            ID: 2,
            Ranking: 55,
        },
        {
            ID: 3,
            Ranking: 1,
        }
    ];
    
    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: mock
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });
    
    let list = container.querySelector('#stats-table');
    let listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(mock.length);
    
    fireEvent.click(container.querySelector('#filter-top-10'));

    list = container.querySelector('#stats-table');
    listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(2);
});

test('can filter by top 20', async () => {
    jest.mock("axios");
    axios.get = jest.fn();

    let mock = [
        {
            ID: 1,
            Ranking: 4,
        },
        {
            ID: 2,
            Ranking: 55,
        },
        {
            ID: 3,
            Ranking: 1,
        },
        {
            ID: 4,
            Ranking: 15,
        }
    ];

    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: mock
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    let list = container.querySelector('#stats-table');
    let listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(mock.length);

    fireEvent.click(container.querySelector('#filter-top-20'));

    list = container.querySelector('#stats-table');
    listItems = list.querySelectorAll('tr');

    expect(list).not.toBeNull();
    expect(listItems.length).toBe(3);
});

test('can filter by top 30', async () => {
    jest.mock("axios");
    axios.get = jest.fn();

    let mock = [
        {
            ID: 1,
            Ranking: 4,
        },
        {
            ID: 2,
            Ranking: 55,
        },
        {
            ID: 3,
            Ranking: 1,
        },
        {
            ID: 4,
            Ranking: 15,
        },
        {
            ID: 5,
            Ranking: 40,
        },
        {
            ID: 6,
            Ranking: 60,
        },
        {
            ID: 7,
            Ranking: 27,
        }
    ];

    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: mock
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    let list = container.querySelector('#stats-table');
    let listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(mock.length);

    fireEvent.click(container.querySelector('#filter-top-30'));

    list = container.querySelector('#stats-table');
    listItems = list.querySelectorAll('tr');

    expect(list).not.toBeNull();
    expect(listItems.length).toBe(4);
});
```

Wyniki statystyk mogą byc także sortowane. Kryteria sortowania określone są po kolumnach: 
- Nazwa
- Ranking
- Ilość poszczególnych gier (Wygrane/Remisy/Przegrane)

Dlatego przetestowaliśmy również i to:
```javascript

import React from "react";
import ReactDOM from 'react-dom';
import {act} from "react-dom/test-utils";
import Stats from "./Stats";
import axios from "axios";
import {fireEvent} from "@testing-library/react";


// tworzę zmienna na konterner
// wyrederowana treść komponentów bedzie znajdowana się tutaj
let container;

// ta funkcja bedzie wykonywałą się przed każdym testem
beforeEach(() => {
    // jako konterner ustanawiam element HTML div
    // następnie dodaje go body w dokumencie
    container = document.createElement("div");
    document.body.appendChild(container);
});

// ta funckja będzie wykonywała się po ką=ażdym teście
afterEach(() => {
    // usuewam z dokumnetu kontener
    // a nastepnie zawartyość jego zmiennej
    // zabopeignie to problemów z
    // renderowaniem przy każdym teście
    document.body.removeChild(container);
    container = null;
});

// test sprawdza czy dane które przyszłby z API
// renderują się poprawnie
test('it renders data from API', async () => {
    // definuje że axios bedzie mockowany
    jest.mock("axios");
    // mowie co konkretnie bedzie mockowane
    axios.get = jest.fn();

    // definuje dane które przyszłyby z API
    // gdybyśmy robili realne zapytanie HTTP
    let mock = {
        ID: 1,
        Avatar: 'https://i.pinimg.com/736x/3b/37/cd/3b37cd80d4f092ed392b1453b64cf0d0.jpg',
        Nazwa: "Testowy Kot",
        Ranking: 1,
        Wygrane: 999,
        Remisy: 0,
        Przegrane: 0
    };

    // UWAGA:
    // komponent Stats wykorzystuje komponent Posts do renderowania wyników API
    // z komponentu Posts wiemy w jaki sposób powinny wygladac dane
    // tj. dlaczego obiekt mock ma akurat taką strukture a nie inną

    // mockuje metode get biblioteki axios jako konkretną implementacje
    // "ej stary, jesli ktoś berdzie probował uzyc Twojej funkcji get() to
    // zamiast wykonywac zapytanie zwroc mu te dane"
    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: [mock]
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    // skoro zmockowalismy dane to wiemy w jakej postaci przysły
    // powinnien byc jeden element z danymi ze zmiennej mock
    const listItem = container.querySelector('#stats-table tr:first-child');
    const statistic = listItem.querySelector('td:last-child');

    expect(listItem).not.toBeNull();
    expect(statistic.innerHTML).toBe(`${mock.Wygrane}/${mock.Remisy}/${mock.Przegrane}`);
});


// test sprawdza filtorowanie po top 10 działa
test('can filter by top 10', async () => {
    // definuje że axios bedzie mockowany
    jest.mock("axios");
    // mowie co konkretnie bedzie mockowane
    axios.get = jest.fn();

    // definuje dane które przyszłyby z API
    // gdybyśmy robili realne zapytanie HTTP
    let mock = [
        {
            ID: 1,
            Ranking: 4,
        },
        {
            ID: 2,
            Ranking: 55,
        },
        {
            ID: 3,
            Ranking: 1,
        }
    ];

    // UWAGA:
    // komponent Stats wykorzystaje komponent Posts do renderowania wyników API
    // z komponentu Posts wiemy w jaki sposób powinne wygladac dane

    // UWAGA:
    // Mozna ogarniczac klucze obiektów do tych które są wymagane przez komponent
    // oraz do testowania, np zeby sprawdzic czy filtrowanie dziala
    // potrzebujemy tylko klucze ID oraz Ranking

    // mockuje metode get biblioteki axios jako konkretną implementacje
    // "ej stary, jesli ktoś berdzie probował uzyc Twojej funkcji get() to
    // zamiast wykonywac zapytanie zwroc mu te dane"
    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: mock
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    // skoro zmockowalismy dane to wiemy w jakej postaci przysły
    // sprawdzamy poczatkowy stan, powinny byc wyrenderowane 3 elementy listy
    let list = container.querySelector('#stats-table');
    let listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(mock.length);

    // klikamy przycisk do filtracji po top 10
    fireEvent.click(container.querySelector('#filter-top-10'));

    list = container.querySelector('#stats-table');
    listItems = list.querySelectorAll('tr');
    // lista statysk powinna zawierac 2 elementy listy
    // poniewaz ranking tylko dwóch gracz jest mniejszy, rowny 10
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(2);
});

// test sprawdza filtorowanie po top 20 działa
test('can filter by top 20', async () => {
    jest.mock("axios");
    axios.get = jest.fn();

    let mock = [
        {
            ID: 1,
            Ranking: 4,
        },
        {
            ID: 2,
            Ranking: 55,
        },
        {
            ID: 3,
            Ranking: 1,
        },
        {
            ID: 4,
            Ranking: 15,
        }
    ];

    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: mock
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    let list = container.querySelector('#stats-table');
    let listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(mock.length);

    fireEvent.click(container.querySelector('#filter-top-20'));

    list = container.querySelector('#stats-table');
    listItems = list.querySelectorAll('tr');

    expect(list).not.toBeNull();
    expect(listItems.length).toBe(3);
});

// test sprawdza filtorowanie po top 30 działa
test('can filter by top 30', async () => {
    jest.mock("axios");
    axios.get = jest.fn();

    let mock = [
        {
            ID: 1,
            Ranking: 4,
        },
        {
            ID: 2,
            Ranking: 55,
        },
        {
            ID: 3,
            Ranking: 1,
        },
        {
            ID: 4,
            Ranking: 15,
        },
        {
            ID: 5,
            Ranking: 40,
        },
        {
            ID: 6,
            Ranking: 60,
        },
        {
            ID: 7,
            Ranking: 27,
        }
    ];

    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: mock
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    let list = container.querySelector('#stats-table');
    let listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(mock.length);

    fireEvent.click(container.querySelector('#filter-top-30'));

    list = container.querySelector('#stats-table');
    listItems = list.querySelectorAll('tr');

    expect(list).not.toBeNull();
    expect(listItems.length).toBe(4);
});

// test sprawdza filtorowanie po top 50 działa
test('can filter by top 50', async () => {
    jest.mock("axios");
    axios.get = jest.fn();

    let mock = [
        {
            ID: 1,
            Ranking: 4,
        },
        {
            ID: 2,
            Ranking: 55,
        },
        {
            ID: 3,
            Ranking: 1,
        },
        {
            ID: 4,
            Ranking: 15,
        },
        {
            ID: 5,
            Ranking: 40,
        },
        {
            ID: 6,
            Ranking: 60,
        },
        {
            ID: 7,
            Ranking: 27,
        }
    ];

    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: mock
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    let list = container.querySelector('#stats-table');
    let listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(mock.length);

    fireEvent.click(container.querySelector('#filter-top-50'));

    list = container.querySelector('#stats-table');
    listItems = list.querySelectorAll('tr');

    expect(list).not.toBeNull();
    expect(listItems.length).toBe(5);
});

// test sprawdza sortowanie po nazwie rosnąco
test('Sorting up by name works properly', async () => {
    jest.mock("axios");
    axios.get = jest.fn();

    let mock = [
        {
            ID: 1,
            Avatar: 'https:avatar0.jpg',
            Nazwa: "username0",
        },
        {
            ID: 2,
            Avatar: 'https:avatar2.jpg',
            Nazwa: "username2",
        },
        {
            ID: 3,
            Avatar: 'https:avatar1.jpg',
            Nazwa: "username1",
        },
        {
            ID: 4,
            Avatar: 'https:avatar3.jpg',
            Nazwa: "username3",
        }
    ];

    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: mock
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    let list = container.querySelector('#stats-table');
    let listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(mock.length);

    fireEvent.click(container.querySelector('#sort-up-by-name'));

    list = container.querySelector('#stats-table'); //cała tablica (już posortowana)
    listItems = list.querySelectorAll('tr'); //wybieram wszystkie wiersze
    let personalinfo0 = listItems[0].querySelector('td:first-child'); //od pierwszego użytkownika (w już posortowanej liście)
    let personalinfo1 = listItems[1].querySelector('td:first-child'); //od drugiego użytkownika
    let personalinfo2 = listItems[2].querySelector('td:first-child');
    let personalinfo3 = listItems[3].querySelector('td:first-child');

    expect(listItems).not.toBeNull();
    expect(personalinfo0.innerHTML).toBe(`${mock[0].ID} <img src=\"https:avatar0.jpg\" width=\"50\" height=\"50\"> ${mock[0].Nazwa} `);
    expect(personalinfo1.innerHTML).toBe(`${mock[2].ID} <img src=\"https:avatar1.jpg\" width=\"50\" height=\"50\"> ${mock[2].Nazwa} `);
    expect(personalinfo2.innerHTML).toBe(`${mock[1].ID} <img src=\"https:avatar2.jpg\" width=\"50\" height=\"50\"> ${mock[1].Nazwa} `);
    expect(personalinfo3.innerHTML).toBe(`${mock[3].ID} <img src=\"https:avatar3.jpg\" width=\"50\" height=\"50\"> ${mock[3].Nazwa} `);
});

test('Sorting up by ranking position works properly', async () => {
    jest.mock("axios");
    axios.get = jest.fn();

    let mock = [
        {
            ID: 1,
            Ranking: 3,
        },
        {
            ID: 2,
            Ranking: 5,
        },
        {
            ID: 3,
            Ranking: 1,
        },
        {
            ID: 4,
            Ranking: 4,
        }
    ];

    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: mock
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    let list = container.querySelector('#stats-table');
    let listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(mock.length);

    fireEvent.click(container.querySelector('#sort-up-by-rank'));

    list = container.querySelector('#stats-table'); //cała tablica (już posortowana)
    listItems = list.querySelectorAll('tr'); //wybieram wszystkie wiersze
    let personalinfo0 = listItems[0].querySelector('td:nth-child(2)'); //od pierwszego użytkownika (w już posortowanej liście)
    let personalinfo1 = listItems[1].querySelector('td:nth-child(2)'); //od drugiego użytkownika
    let personalinfo2 = listItems[2].querySelector('td:nth-child(2)');
    let personalinfo3 = listItems[3].querySelector('td:nth-child(2)');

    expect(listItems).not.toBeNull();
    expect(personalinfo0.innerHTML).toBe(`${mock[2].Ranking}`);
    expect(personalinfo1.innerHTML).toBe(`${mock[0].Ranking}`);
    expect(personalinfo2.innerHTML).toBe(`${mock[3].Ranking}`);
    expect(personalinfo3.innerHTML).toBe(`${mock[1].Ranking}`);
});

test('Sorting up by number of win games works properly', async () => {
    jest.mock("axios");
    axios.get = jest.fn();

    let mock = [
        {
            ID: 1,
            Wygrane: 3,
            Remisy: 0,
            Przegrane: 1,
        },
        {
            ID: 2,
            Wygrane: 5,
            Remisy: 7,
            Przegrane: 5,
        },
        {
            ID: 3,
            Wygrane: 1,
            Remisy: 3,
            Przegrane: 0,
        },
        {
            ID: 4,
            Wygrane: 5,
            Remisy: 10,
            Przegrane: 100,
        }
    ];

    await act(async () => {
        await axios.get.mockImplementationOnce(() => Promise.resolve({
            data: mock
        }));
        ReactDOM.render(<Stats effect={100}/>, container);
    });

    let list = container.querySelector('#stats-table');
    let listItems = list.querySelectorAll('tr');
    expect(list).not.toBeNull();
    expect(listItems.length).toBe(mock.length);

    fireEvent.click(container.querySelector('#sort-up-by-wins'));

    list = container.querySelector('#stats-table'); //cała tablica (już posortowana)
    listItems = list.querySelectorAll('tr'); //wybieram wszystkie wiersze
    let personalinfo0 = listItems[0].querySelector('td:last-child'); //od pierwszego użytkownika (w już posortowanej liście)
    let personalinfo1 = listItems[1].querySelector('td:last-child'); //od drugiego użytkownika
    let personalinfo2 = listItems[2].querySelector('td:last-child');
    let personalinfo3 = listItems[3].querySelector('td:last-child');

    expect(listItems).not.toBeNull();
    expect(personalinfo0.innerHTML).toBe(`${mock[2].Wygrane}/${mock[2].Remisy}/${mock[2].Przegrane}`);
    expect(personalinfo1.innerHTML).toBe(`${mock[0].Wygrane}/${mock[0].Remisy}/${mock[0].Przegrane}`);
    expect(personalinfo2.innerHTML).toBe(`${mock[1].Wygrane}/${mock[1].Remisy}/${mock[1].Przegrane}`);
    expect(personalinfo3.innerHTML).toBe(`${mock[3].Wygrane}/${mock[3].Remisy}/${mock[3].Przegrane}`);
});
```