<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pablo and Felix' Pizza Reviews</title>
    <style>
        :root {
            --bg: #ffffff;
            --text: #1a1a1a;
            --card-bg: #f5f5f5;
            --border: #d0d0d0;
            --accent: #5d3a6f;
            --hover-bg: #5d3a6f;
            --hover-text: #ffffff;
        }

        [data-theme="dark"] {
            --bg: #0a0a0a;
            --text: #e8e8e8;
            --card-bg: #1a1a1a;
            --border: #2a2a2a;
            --accent: #7d5a8f;
            --hover-bg: #7d5a8f;
            --hover-text: #ffffff;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: var(--bg);
            color: var(--text);
            transition: background 0.3s, color 0.3s;
            padding: 40px 20px;
            line-height: 1.6;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        header {
            margin-bottom: 50px;
        }

        h1 {
            font-size: 3em;
            margin-bottom: 10px;
            color: var(--accent);
            font-weight: 700;
        }

        .subtitle {
            font-size: 1.2em;
            color: var(--text);
            opacity: 0.8;
        }

        .rules {
            background: var(--card-bg);
            padding: 30px;
            margin-bottom: 40px;
            border: 2px solid var(--border);
        }

        .rules h2 {
            margin-bottom: 20px;
            color: var(--accent);
            font-size: 1.5em;
        }

        .rules ol {
            margin-left: 25px;
        }

        .rules li {
            margin: 15px 0;
        }

        .rules ul {
            margin: 10px 0 10px 25px;
        }

        .controls {
            display: flex;
            gap: 20px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .theme-toggle {
            background: var(--accent);
            color: white;
            border: 2px solid var(--accent);
            padding: 12px 24px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: background 0.4s, color 0.4s;
        }

        .theme-toggle:hover {
            background: var(--bg);
            color: var(--accent);
        }

        .search-box {
            flex: 1;
            min-width: 250px;
            padding: 12px;
            border: 2px solid var(--border);
            background: var(--card-bg);
            color: var(--text);
            font-size: 16px;
            transition: border-color 0.3s;
        }

        .search-box:focus {
            outline: none;
            border-color: var(--accent);
        }

        .table-container {
            overflow-x: auto;
            border: 2px solid var(--border);
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th {
            background: var(--accent);
            color: white;
            padding: 16px;
            text-align: left;
            cursor: pointer;
            user-select: none;
            font-weight: 600;
            border-right: 2px solid rgba(255,255,255,0.2);
            transition: background 0.4s, color 0.4s;
        }

        th:last-child {
            border-right: none;
        }

        th:hover {
            background: var(--bg);
            color: var(--accent);
        }

        th::after {
            content: ' ⇅';
            opacity: 0.6;
            margin-left: 5px;
        }

        th.sort-asc::after {
            content: ' ↑';
            opacity: 1;
        }

        th.sort-desc::after {
            content: ' ↓';
            opacity: 1;
        }

        td {
            padding: 16px;
            border-bottom: 1px solid var(--border);
            border-right: 1px solid var(--border);
            transition: background 0.4s, color 0.4s;
        }

        td:last-child {
            border-right: none;
        }

        tbody tr {
            background: var(--bg);
            transition: background 0.4s, color 0.4s;
        }

        tbody tr:hover {
            background: var(--hover-bg);
            color: var(--hover-text);
        }

        tbody tr:hover a {
            color: var(--hover-text);
        }

        .rating {
            font-weight: 700;
            color: var(--accent);
        }

        tbody tr:hover .rating {
            color: var(--hover-text);
        }

        a {
            color: var(--accent);
            text-decoration: none;
            font-weight: 600;
            transition: color 0.4s;
        }

        a:hover {
            text-decoration: underline;
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 2em;
            }
            
            th, td {
                padding: 12px 8px;
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🍕 Pablo and Felix' Pizza Reviews</h1>
            <p class="subtitle">Rating pizzas, one slice at a time</p>
        </header>

        <div class="rules">
            <h2>The 3 Simple Rules:</h2>
            <ol>
                <li>Every Pizza gets <b>2 ratings from 0.0 to 10.0</b>, one for the general quality of the pizza (GQ) and one for the value offered (VO)</li>
                <li>The rating scale is normalized to the Freiburger Mensa Institutsviertel Buffet Pizza which is evaluated at:
                    <ul>
                        <li><b>General quality (GQ): 5.0/10</b></li>
                        <li><b>Value offered (VO): 7.0/10</b> (5.9€ as of 01.11.2025)</li>
                    </ul>
                </li>
                <li>The ambience of the restaurant, friendliness of the staff, options on the menu, blablabla, [...] <b><ins>do not have any influence</ins></b> on these ratings!</li>
            </ol>
        </div>

        <div class="controls">
            <button class="theme-toggle" onclick="toggleTheme()">🌓 Toggle Dark Mode</button>
            <input type="text" class="search-box" placeholder="Search restaurants..." onkeyup="filterTable()">
        </div>

        <div class="table-container">
            <table id="pizzaTable">
                <thead>
                    <tr>
                        <th onclick="sortTable(0)">ID</th>
                        <th onclick="sortTable(1)">Name</th>
                        <th onclick="sortTable(2)">Location</th>
                        <th onclick="sortTable(3)">GQ</th>
                        <th onclick="sortTable(4)">VO</th>
                        <th>Website</th>
                        <th>Picture</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>0000</td>
                        <td>Mensa</td>
                        <td>Freiburg</td>
                        <td class="rating">5.0</td>
                        <td class="rating">7.0</td>
                        <td><a href="https://www.swfr.de/essen/mensen-cafes-speiseplaene/freiburg/mensa-institutsviertel" target="_blank">Visit</a></td>
                        <td>Will come</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

    <script>
        function toggleTheme() {
            const html = document.documentElement;
            const currentTheme = html.getAttribute('data-theme');
            const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
            html.setAttribute('data-theme', newTheme);
            localStorage.setItem('theme', newTheme);
        }

        const savedTheme = localStorage.getItem('theme') || 'light';
        document.documentElement.setAttribute('data-theme', savedTheme);

        let sortDirection = {};

        function sortTable(columnIndex) {
            const table = document.getElementById('pizzaTable');
            const tbody = table.querySelector('tbody');
            const rows = Array.from(tbody.querySelectorAll('tr'));
            
            sortDirection[columnIndex] = sortDirection[columnIndex] === 'asc' ? 'desc' : 'asc';
            
            const headers = table.querySelectorAll('th');
            headers.forEach(h => h.className = '');
            headers[columnIndex].className = 'sort-' + sortDirection[columnIndex];
            
            rows.sort((a, b) => {
                let aVal = a.cells[columnIndex].textContent.trim();
                let bVal = b.cells[columnIndex].textContent.trim();
                
                const aNum = parseFloat(aVal);
                const bNum = parseFloat(bVal);
                if (!isNaN(aNum) && !isNaN(bNum)) {
                    return sortDirection[columnIndex] === 'asc' ? aNum - bNum : bNum - aNum;
                }
                
                return sortDirection[columnIndex] === 'asc' 
                    ? aVal.localeCompare(bVal) 
                    : bVal.localeCompare(aVal);
            });
            
            rows.forEach(row => tbody.appendChild(row));
        }

        function filterTable() {
            const input = document.querySelector('.search-box');
            const filter = input.value.toLowerCase();
            const table = document.getElementById('pizzaTable');
            const rows = table.querySelectorAll('tbody tr');
            
            rows.forEach(row => {
                const text = row.textContent.toLowerCase();
                row.style.display = text.includes(filter) ? '' : 'none';
            });
        }
    </script>
</body>
</html>
