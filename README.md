<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pablo and Felix' Pizza Reviews</title>
    <style>
        :root {
            --bg: #ffffff;
            --text: #2c3e50;
            --card-bg: #f8f9fa;
            --border: #e1e4e8;
            --accent: #e74c3c;
            --hover: #f5f5f5;
        }

        [data-theme="dark"] {
            --bg: #1a1a1a;
            --text: #e0e0e0;
            --card-bg: #2d2d2d;
            --border: #404040;
            --accent: #ff6b6b;
            --hover: #3a3a3a;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
            background: var(--bg);
            color: var(--text);
            transition: background 0.3s, color 0.3s;
            padding: 20px;
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 40px;
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            color: var(--accent);
        }

        .rules {
            background: var(--card-bg);
            padding: 25px;
            border-radius: 12px;
            margin-bottom: 30px;
            border: 1px solid var(--border);
        }

        .rules h2 {
            margin-bottom: 15px;
        }

        .rules ol {
            margin-left: 20px;
        }

        .rules li {
            margin: 10px 0;
        }

        .controls {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            align-items: center;
        }

        .theme-toggle {
            background: var(--accent);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            transition: opacity 0.3s;
        }

        .theme-toggle:hover {
            opacity: 0.9;
        }

        .search-box {
            flex: 1;
            min-width: 200px;
            padding: 10px;
            border: 1px solid var(--border);
            border-radius: 8px;
            background: var(--card-bg);
            color: var(--text);
            font-size: 16px;
        }

        .table-container {
            overflow-x: auto;
            background: var(--card-bg);
            border-radius: 12px;
            border: 1px solid var(--border);
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        th {
            background: var(--accent);
            color: white;
            padding: 15px;
            text-align: left;
            cursor: pointer;
            user-select: none;
            position: sticky;
            top: 0;
        }

        th:hover {
            opacity: 0.9;
        }

        th::after {
            content: ' ⇅';
            opacity: 0.5;
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
            padding: 15px;
            border-bottom: 1px solid var(--border);
        }

        tr:hover {
            background: var(--hover);
        }

        .rating {
            font-weight: bold;
            color: var(--accent);
        }

        a {
            color: var(--accent);
            text-decoration: none;
        }

        a:hover {
            text-decoration: underline;
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 1.8em;
            }
            
            th, td {
                padding: 10px;
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🍕 Pablo and Felix' Pizza Review Site</h1>
            <p>We rate pizza restaurants on this site.</p>
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
