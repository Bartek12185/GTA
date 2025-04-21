# GTA<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GTA 5 – Auta na sprzedaż</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>GTA 5 – Auta na sprzedaż</h1>
        <p>Znajdź swój wymarzony pojazd prosto z Los Santos!</p>
    </header>

    <main>
        <section class="filters">
            <label for="typeFilter">Typ:</label>
            <select id="typeFilter">
                <option value="all">Wszystkie</option>
                <option value="supersamochód">Supersamochód</option>
                <option value="sportowy">Sportowy</option>
                <option value="terenowy">Terenowy</option>
            </select>

            <label for="sortPrice">Cena:</label>
            <select id="sortPrice">
                <option value="default">Domyślnie</option>
                <option value="asc">Rosnąco</option>
                <option value="desc">Malejąco</option>
            </select>

            <input type="text" id="search" placeholder="Szukaj po nazwie...">
        </section>

        <section class="car-list" id="carList">
            <!-- Karty aut -->
            <div class="car" data-type="supersamochód" data-price="4500000" data-name="Truffade Adder">
                <img src="https://static.wikia.nocookie.net/gtawiki/images/0/0b/Adder-GTAV-FrontQuarter.png" alt="Truffade Adder">
                <h2>Truffade Adder</h2>
                <p>Supersamochód z niesamowitym przyspieszeniem i osiągami.</p>
                <span class="price">4 500 000 zł</span>
                <button>Kup teraz</button>
            </div>

            <div class="car" data-type="sportowy" data-price="450000" data-name="Annis Elegy RH8">
                <img src="https://static.wikia.nocookie.net/gtawiki/images/4/4a/ElegyRH8-GTAV-FrontQuarter.png" alt="Annis Elegy RH8">
                <h2>Annis Elegy RH8</h2>
                <p>Sportowy klasyk, znany z doskonałego prowadzenia.</p>
                <span class="price">450 000 zł</span>
                <button>Kup teraz</button>
            </div>

            <div class="car" data-type="terenowy" data-price="600000" data-name="Coil Brawler">
                <img src="https://static.wikia.nocookie.net/gtawiki/images/f/f1/Brawler-GTAO-FrontQuarter.png" alt="Coil Brawler">
                <h2>Coil Brawler</h2>
                <p>Wytrzymały terenowiec stworzony do jazdy po bezdrożach.</p>
                <span class="price">600 000 zł</span>
                <button>Kup teraz</button>
            </div>
        </section>
    </main>

    <footer>
        <p>&copy; 2025 GTA Motors. Niepowiązane z Rockstar Games.</p>
    </footer>

    <script>
        const typeFilter = document.getElementById("typeFilter");
        const sortPrice = document.getElementById("sortPrice");
        const search = document.getElementById("search");
        const carList = document.getElementById("carList");

        let cars = Array.from(document.querySelectorAll(".car"));

        function updateDisplay() {
            const selectedType = typeFilter.value;
            const searchTerm = search.value.toLowerCase();
            const sortValue = sortPrice.value;

            let filteredCars = cars.filter(car => {
                const type = car.getAttribute("data-type");
                const name = car.getAttribute("data-name").toLowerCase();

                const matchesType = selectedType === "all" || selectedType === type;
                const matchesSearch = name.includes(searchTerm);

                return matchesType && matchesSearch;
            });

            if (sortValue === "asc") {
                filteredCars.sort((a, b) => a.getAttribute("data-price") - b.getAttribute("data-price"));
            } else if (sortValue === "desc") {
                filteredCars.sort((a, b) => b.getAttribute("data-price") - a.getAttribute("data-price"));
            }

            carList.innerHTML = "";
            filteredCars.forEach(car => carList.appendChild(car));
        }

        typeFilter.addEventListener("change", updateDisplay);
        sortPrice.addEventListener("change", updateDisplay);
        search.addEventListener("input", updateDisplay);
    </script>
</body>
</html>.filters {
    text-align: center;
    margin: 20px 0;
}

.filters label, .filters select, .filters input {
    margin: 5px 10px;
    font-size: 16px;
}

.filters select, .filters input {
    padding: 8px 12px;
    border-radius: 5px;
    border: none;
    background-color: #222;
    color: #fff;
}
