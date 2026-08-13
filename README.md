<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BH REALM - Web Gaming Hub (12+)</title>
    <style>
        :root {
            --bg-dark: #0a0b10;
            --bg-panel: #121522;
            --bg-card: #181c2e;
            --accent: #00ffcc;
            --accent-hover: #00cca3;
            --text-main: #ffffff;
            --text-muted: #8e95a5;
            --border: #23283e;
            --font: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-main);
            font-family: var(--font);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        header {
            background: var(--bg-panel);
            padding: 20px 40px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid var(--accent);
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .logo h1 {
            color: var(--accent);
            font-size: 1.8rem;
        }

        .logo p {
            color: var(--text-muted);
            font-size: 0.85rem;
        }

        .controls {
            display: flex;
            gap: 15px;
        }

        .controls input, .controls select {
            background: var(--bg-dark);
            border: 1px solid var(--border);
            color: #fff;
            padding: 10px 15px;
            border-radius: 8px;
            outline: none;
            transition: 0.2s ease;
        }

        .controls input:focus, .controls select:focus {
            border-color: var(--accent);
        }

        .container {
            max-width: 1400px;
            width: 100%;
            margin: 0 auto;
            padding: 30px 20px;
            flex: 1;
        }

        .category-section {
            margin-bottom: 40px;
        }

        .category-title {
            color: var(--accent);
            font-size: 1.5rem;
            margin-bottom: 15px;
            border-bottom: 1px solid var(--border);
            padding-bottom: 8px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
            gap: 20px;
        }

        .card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 10px;
            padding: 18px;
            text-decoration: none;
            color: #fff;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            transition: transform 0.2s, border-color 0.2s;
        }

        .card:hover {
            transform: translateY(-4px);
            border-color: var(--accent);
        }

        .card h3 {
            color: #fff;
            font-size: 1.1rem;
            margin-bottom: 6px;
        }

        .card p {
            color: var(--text-muted);
            font-size: 0.85rem;
            margin-bottom: 12px;
        }

        .card-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .badge {
            background: var(--bg-panel);
            color: var(--accent);
            border: 1px solid var(--border);
            padding: 3px 8px;
            border-radius: 4px;
            font-size: 0.75rem;
        }

        .play-btn {
            background: var(--accent);
            color: #000;
            font-weight: bold;
            padding: 4px 10px;
            border-radius: 4px;
            font-size: 0.8rem;
        }

        footer {
            text-align: center;
            padding: 20px;
            color: var(--text-muted);
            background: var(--bg-panel);
            border-top: 1px solid var(--border);
            font-size: 0.85rem;
        }
    </style>
</head>
<body>

    <header>
        <div class="logo">
            <h1>BH REALM</h1>
            <p>100 Games | 10 Categories | Direct Web Play</p>
        </div>
        <div class="controls">
            <select id="categoryFilter" onchange="filterGames()">
                <option value="ALL">All Categories</option>
                <option value="Action">Action</option>
                <option value="Racing">Racing</option>
                <option value="Strategy">Strategy</option>
                <option value="Puzzle">Puzzle</option>
                <option value="RPG">RPG</option>
                <option value="Arcade">Arcade</option>
                <option value="Sports">Sports</option>
                <option value="Simulation">Simulation</option>
                <option value="Adventure">Adventure</option>
                <option value="Sci-Fi">Sci-Fi</option>
            </select>
            <input type="text" id="searchInput" onkeyup="filterGames()" placeholder="Search game title...">
        </div>
    </header>

    <main class="container" id="catalogContainer">
        </main>

    <footer>
        <p>&copy; 2026 BH REALM. Rated 12+ Gaming Catalog.</p>
    </footer>

    <script>
        // Catalog mapping real individual game titles directly to their respective web game URLs
        const gamesCatalog = [
            // ACTION
            { id: 1, title: "Superhot Prototype", category: "Action", desc: "Time moves only when you move in this shooter.", url: "https://www.crazygames.com/game/superhot-prototype" },
            { id: 2, title: "Time Shooter 2", category: "Action", desc: "Action fps with time manipulation mechanics.", url: "https://www.crazygames.com/game/time-shooter-2" },
            { id: 3, title: "Venge.io", category: "Action", desc: "Fast-paced multiplayer objective-based shooter.", url: "https://venge.io" },
            { id: 4, title: "Subway Surfers", category: "Action", desc: "Run, dodge trains, and collect coins in this classic runner.", url: "https://poki.com/en/g/subway-surfers" },
            { id: 5, title: "Temple Run 2", category: "Action", desc: "Navigate hazardous cliffs, zip lines, and mines.", url: "https://poki.com/en/g/temple-run-2" },
            { id: 6, title: "Stickman Hook", category: "Action", desc: "Swing through hundreds of challenging stickman levels.", url: "https://poki.com/en/g/stickman-hook" },
            { id: 7, title: "Vex 7", category: "Action", desc: "High-speed parkour stickman obstacle runner.", url: "https://www.crazygames.com/game/vex-7" },
            { id: 8, title: "Ev.io", category: "Action", desc: "Futuristic arena shooter set in sci-fi environments.", url: "https://ev.io" },
            { id: 9, title: "Getaway Shootout", category: "Action", desc: "Race to the extraction vehicle against three others.", url: "https://www.crazygames.com/game/getaway-shootout" },
            { id: 10, title: "Bullet Force", category: "Action", desc: "FPS featuring tactical team combat and vehicles.", url: "https://www.crazygames.com/game/bullet-force-multiplayer" },

            // RACING
            { id: 11, title: "Moto X3M", category: "Racing", desc: "Perform stunts over explosive obstacle tracks.", url: "https://poki.com/en/g/moto-x3m" },
            { id: 12, title: "Madalin Stunt Cars 2", category: "Racing", desc: "Drive sports cars across open-world stunt arenas.", url: "https://www.crazygames.com/game/madalin-stunt-cars-2" },
            { id: 13, title: "Drift Hunters", category: "Racing", desc: "Tune cars and score high points on drifting tracks.", url: "https://www.crazygames.com/game/drift-hunters" },
            { id: 14, title: "Mr Racer", category: "Racing", desc: "High speed highway traffic racing game.", url: "https://www.crazygames.com/game/mr-racer" },
            { id: 15, title: "Drive Mad", category: "Racing", desc: "Drive over obstacles without flipping your truck.", url: "https://poki.com/en/g/drive-mad" },
            { id: 16, title: "Cyber Cars Punk Racing", category: "Racing", desc: "Futuristic racing through neon city streets.", url: "https://www.crazygames.com/game/cyber-cars-punk-racing" },
            { id: 17, title: "Highway Traffic", category: "Racing", desc: "Weave through oncoming highway traffic at top speed.", url: "https://www.crazygames.com/game/highway-traffic" },
            { id: 18, title: "Racing Horizon", category: "Racing", desc: "Unlimited highway driving with multiple car modes.", url: "https://www.crazygames.com/game/racing-horizon" },
            { id: 19, title: "Super Bike The Champion", category: "Racing", desc: "Compete in fast-paced motorcycling grand prix.", url: "https://www.crazygames.com/game/super-bike-the-champion" },
            { id: 20, title: "Rush Race", category: "Racing", desc: "Simple turn-and-lane switching arcade racing.", url: "https://poki.com/en/g/rush-race" },

            // STRATEGY
            { id: 21, title: "Tower Defense Clash", category: "Strategy", desc: "Build defense towers to protect your castle.", url: "https://www.crazygames.com/game/tower-defense-clash" },
            { id: 22, title: "Bloons Tower Defense 4", category: "Strategy", desc: "Place monkey towers to pop incoming balloon waves.", url: "https://www.crazygames.com/game/bloons-tower-defense-4" },
            { id: 23, title: "Chess Free", category: "Strategy", desc: "Play classic chess against varying AI levels.", url: "https://poki.com/en/g/chess" },
            { id: 24, title: "Master Checkers", category: "Strategy", desc: "Standard checkers logic game.", url: "https://poki.com/en/g/master-checkers" },
            { id: 25, title: "State.io", category: "Strategy", desc: "Conquer territory in tactical real-time strategy.", url: "https://www.crazygames.com/game/state-io" },
            { id: 26, title: "City Siege", category: "Strategy", desc: "Tactical unit deployment to rescue hostages.", url: "https://www.crazygames.com/game/city-siege" },
            { id: 27, title: "Battleship", category: "Strategy", desc: "Find and sink enemy naval ships.", url: "https://poki.com/en/g/battleship" },
            { id: 28, title: "Age of War", category: "Strategy", desc: "Evolve your base through ages from cavemen to future.", url: "https://www.crazygames.com/game/age-of-war" },
            { id: 29, title: "Risk of War", category: "Strategy", desc: "Turn-based map conquest strategy.", url: "https://www.crazygames.com/game/risk-of-war" },
            { id: 30, title: "Endless Siege", category: "Strategy", desc: "Daily new tower defense map challenges.", url: "https://www.crazygames.com/game/endless-siege" },

            // PUZZLE
            { id: 31, title: "2048", category: "Puzzle", desc: "Combine identical numbered tiles to reach 2048.", url: "https://poki.com/en/g/2048" },
            { id: 32, title: "Cut The Rope", category: "Puzzle", desc: "Cut ropes to feed candy to Om Nom.", url: "https://poki.com/en/g/cut-the-rope" },
            { id: 33, title: "Water Sort Puzzle", category: "Puzzle", desc: "Sort colored liquids into matching tubes.", url: "https://www.crazygames.com/game/water-sort-puzzle" },
            { id: 34, title: "Unblock Me", category: "Puzzle", desc: "Slide wooden blocks to clear a path for the red block.", url: "https://poki.com/en/g/unblock-me" },
            { id: 35, title: "Master Sudoku", category: "Puzzle", desc: "Classic number placement grid puzzle.", url: "https://poki.com/en/g/master-sudoku" },
            { id: 36, title: "Wordle Unlimited", category: "Puzzle", desc: "Guess five-letter secret words in 6 tries.", url: "https://www.crazygames.com/game/wordle" },
            { id: 37, title: "Bubble Shooter", category: "Puzzle", desc: "Match 3 or more bubbles to pop them off the screen.", url: "https://www.crazygames.com/game/bubble-shooter" },
            { id: 38, title: "Brain Test", category: "Puzzle", desc: "Tricky puzzles designed to test logic and creativity.", url: "https://poki.com/en/g/brain-test-tricky-puzzles" },
            { id: 39, title: "Word Chef", category: "Puzzle", desc: "Connect letters together to discover hidden words.", url: "https://poki.com/en/g/word-chef" },
            { id: 40, title: "Mahjong Classic", category: "Puzzle", desc: "Pair matching free tiles to clear the board.", url: "https://poki.com/en/g/mahjong-cards" },

            // RPG
            { id: 41, title: "Hero Wars", category: "RPG", desc: "Battle fantasy monsters and level up hero squads.", url: "https://www.crazygames.com/game/hero-wars" },
            { id: 42, title: "EvoWorld.io", category: "RPG", desc: "Eat food and evolve through levels from fly to dragon.", url: "https://www.crazygames.com/game/flyordie-io" },
            { id: 43, title: "Chibi Knight", category: "RPG", desc: "Side-scrolling fantasy quest adventure.", url: "https://www.crazygames.com/game/chibi-knight" },
            { id: 44, title: "Dungeon Miner", category: "RPG", desc: "Mine resources underground to craft dungeon armor.", url: "https://www.crazygames.com/game/dungeon-miner" },
            { id: 45, title: "Monster Sanctuary", category: "RPG", desc: "Collect monsters and fight turn-based tactical battles.", url: "https://www.crazygames.com/game/monster-sanctuary" },
            { id: 46, title: "Stickman RPG", category: "RPG", desc: "Life simulation role-playing game.", url: "https://www.crazygames.com/game/stickman-rpg" },
            { id: 47, title: "Sword Life", category: "RPG", desc: "Upgrade your blade to slash through fantasy bosses.", url: "https://www.crazygames.com/game/sword-life" },
            { id: 48, title: "Quest for Milk", category: "RPG", desc: "Story-driven indie RPG exploration game.", url: "https://www.crazygames.com/game/quest-for-milk" },
            { id: 49, title: "Clicker Heroes", category: "RPG", desc: "Idle clicker RPG against monsters.", url: "https://www.crazygames.com/game/clicker-heroes" },
            { id: 50, title: "Soul Knight", category: "RPG", desc: "Dungeon crawler with magic and gun upgrades.", url: "https://www.crazygames.com/game/soul-knight" },

            // ARCADE
            { id: 51, title: "PAC-MAN", category: "Arcade", desc: "Eat dots while dodging ghosts in retro mazes.", url: "https://poki.com/en/g/pac-man" },
            { id: 52, title: "Space Invaders", category: "Arcade", desc: "Defend against descending alien waves.", url: "https://www.crazygames.com/game/space-invaders" },
            { id: 53, title: "Flappy Bird", category: "Arcade", desc: "Fly between green pipe obstacles.", url: "https://www.crazygames.com/game/flappy-bird" },
            { id: 54, title: "Geometry Dash", category: "Arcade", desc: "Rhythm-based platform jumping obstacles.", url: "https://www.crazygames.com/game/geometry-dash" },
            { id: 55, title: "Snake.io", category: "Arcade", desc: "Grow longer by consuming glowing dots without crashing.", url: "https://www.crazygames.com/game/snake-io" },
            { id: 56, title: "Slither.io", category: "Arcade", desc: "Classic worm multiplayer arcade survival.", url: "https://slither.io" },
            { id: 57, title: "Paper.io 2", category: "Arcade", desc: "Claim territory on the map by drawing loops.", url: "https://poki.com/en/g/paper-io-2" },
            { id: 58, title: "Crossy Road", category: "Arcade", desc: "Cross busy highways and rivers safely.", url: "https://poki.com/en/g/crossy-road" },
            { id: 59, title: "Doodle Jump", category: "Arcade", desc: "Jump continuously upward on moving platforms.", url: "https://poki.com/en/g/doodle-jump" },
            { id: 60, title: "Fruit Ninja", category: "Arcade", desc: "Slice flying fruits with quick swipe gestures.", url: "https://poki.com/en/g/fruit-ninja" },

            // SPORTS
            { id: 61, title: "Basketball Stars", category: "Sports", desc: "Play 1v1 basketball with famous characters.", url: "https://poki.com/en/g/basketball-stars" },
            { id: 62, title: "A Small World Cup", category: "Sports", desc: "Ragdoll physics 1v1 soccer matches.", url: "https://poki.com/en/g/a-small-world-cup" },
            { id: 63, title: "Golf Champions", category: "Sports", desc: "Mini-golf courses with bank shots.", url: "https://poki.com/en/g/golf-champions" },
            { id: 64, title: "Retro Bowl", category: "Sports", desc: "Retro-styled American football management and play.", url: "https://poki.com/en/g/retro-bowl" },
            { id: 65, title: "Penalty Shooters 2", category: "Sports", desc: "Score penalty kicks and defend goals.", url: "https://www.crazygames.com/game/penalty-shooters-2" },
            { id: 66, title: "Table Tennis World Tour", category: "Sports", desc: "Compete in ping-pong tournaments.", url: "https://www.crazygames.com/game/table-tennis-world-tour" },
            { id: 67, title: "8 Ball Billiards", category: "Sports", desc: "Pocket all target pool balls into table pockets.", url: "https://www.crazygames.com/game/8-ball-billiards-classic" },
            { id: 68, title: "Classic Bowling", category: "Sports", desc: "Line up spin and power for 10-pin bowling strikes.", url: "https://www.crazygames.com/game/classic-bowling" },
            { id: 69, title: "Tennis Masters", category: "Sports", desc: "Fast 2D tennis matches with power-ups.", url: "https://poki.com/en/g/tennis-masters" },
            { id: 70, title: "Air Hockey 3D", category: "Sports", desc: "Defend your goal slit on friction-free air tables.", url: "https://www.crazygames.com/game/air-hockey-3d" },

            // SIMULATION
            { id: 71, title: "BitLife", category: "Simulation", desc: "Text-based life simulator choices.", url: "https://www.crazygames.com/game/bitlife---life-simulator" },
            { id: 72, title: "House Painter", category: "Simulation", desc: "Fill blank building walls with paint rollers.", url: "https://poki.com/en/g/house-painter" },
            { id: 73, title: "Flight Simulator 3D", category: "Simulation", desc: "Pilot commercial aircraft from takeoff to landing.", url: "https://www.crazygames.com/game/flight-simulator-3d" },
            { id: 74, title: "Papa's Pizzeria", category: "Simulation", desc: "Take orders, bake pizzas, and serve customers.", url: "https://www.crazygames.com/game/papas-pizzeria" },
            { id: 75, title: "Farmer Life", category: "Simulation", desc: "Manage crops and farm equipment.", url: "https://www.crazygames.com/game/farmer-life" },
            { id: 76, title: "Supermarket Simulator", category: "Simulation", desc: "Manage inventory, pricing, and checkouts.", url: "https://www.crazygames.com/game/supermarket-simulator" },
            { id: 77, title: "Park Panic", category: "Simulation", desc: "Manage parking lot flow without collisions.", url: "https://poki.com/en/g/park-panic" },
            { id: 78, title: "Idle Mining Empire", category: "Simulation", desc: "Manage miners and upgrade elevator shafts.", url: "https://www.crazygames.com/game/idle-mining-empire" },
            { id: 79, title: "City Airport Flight", category: "Simulation", desc: "Direct runway traffic and flight paths.", url: "https://www.crazygames.com/game/city-airport-flight" },
            { id: 80, title: "Bus Simulator", category: "Simulation", desc: "Pick up passengers and follow city transit routes.", url: "https://www.crazygames.com/game/bus-simulator-ultimate" },

            // ADVENTURE
            { id: 81, title: "Fireboy and Watergirl 1", category: "Adventure", desc: "Cooperative element puzzle-platforming through the Forest Temple.", url: "https://poki.com/en/g/fireboy-and-watergirl-1-forest-temple" },
            { id: 82, title: "Snail Bob", category: "Adventure", desc: "Guide Snail Bob safely through puzzle obstacle stages.", url: "https://poki.com/en/g/snail-bob" },
            { id: 83, title: "Raft Life", category: "Adventure", desc: "Gather floating debris to expand ocean raft shelters.", url: "https://www.crazygames.com/game/raft-life" },
            { id: 84, title: "Fancy Pants Adventures", category: "Adventure", desc: "Fast-paced smooth parkour platformer.", url: "https://poki.com/en/g/fancy-pants-adventure" },
            { id: 85, title: "Castaway Island", category: "Adventure", desc: "Explore uncharted islands to gather tools and survive.", url: "https://www.crazygames.com/game/castaway" },
            { id: 86, title: "Red Ball 4", category: "Adventure", desc: "Roll and bounce through stages to defeat evil squares.", url: "https://poki.com/en/g/red-ball-4" },
            { id: 87, title: "Bob the Robber", category: "Adventure", desc: "Sneak past guards, security cameras, and locks.", url: "https://poki.com/en/g/bob-the-robber" },
            { id: 88, title: "Short Life", category: "Adventure", desc: "Navigate ragdoll physics hazards safely to the end line.", url: "https://www.crazygames.com/game/short-life" },
            { id: 89, title: "Wheely 8", category: "Adventure", desc: "Solve mechanical puzzles to help Wheely reach goals.", url: "https://www.crazygames.com/game/wheely-8" },
            { id: 90, title: "Duck Life 4", category: "Adventure", desc: "Train your racing duck through flying, swimming, and running.", url: "https://www.crazygames.com/game/duck-life-4" },

            // SCI-FI
            { id: 91, title: "Cyberpunk City", category: "Sci-Fi", desc: "Explore neon-lit dystopian cyber environments.", url: "https://www.crazygames.com/game/cyberpunk-city" },
            { id: 92, title: "Space Company", category: "Sci-Fi", desc: "Incremental space technology and orbital resource game.", url: "https://www.crazygames.com/game/space-company" },
            { id: 93, title: "Alien Sky", category: "Sci-Fi", desc: "Shoot down alien fleets across alien planetary skies.", url: "https://www.crazygames.com/game/alien-sky" },
            { id: 94, title: "Laser Overload", category: "Sci-Fi", desc: "Reflect laser beams off mirrors into power batteries.", url: "https://www.crazygames.com/game/laser-overload" },
            { id: 95, title: "Orbital Survival", category: "Sci-Fi", desc: "Maintain orbit while steering clear of space debris.", url: "https://www.crazygames.com/game/orbital-survival" },
            { id: 96, title: "Mech Arena", category: "Sci-Fi", desc: "Battle giant armored walking mechs.", url: "https://www.crazygames.com/game/mech-arena" },
            { id: 97, title: "Starblast.io", category: "Sci-Fi", desc: "Mine asteroids and battle other spaceship pilots.", url: "https://starblast.io" },
            { id: 98, title: "Run 3", category: "Sci-Fi", desc: "Run through 3D spatial tunnels while defying gravity.", url: "https://www.crazygames.com/game/run-3" },
            { id: 99, title: "Solar Smash", category: "Sci-Fi", desc: "Test planetary destruction technology in orbit.", url: "https://www.crazygames.com/game/solar-smash" },
            { id: 100, title: "Space Waves", category: "Sci-Fi", desc: "Rhythm spatial flight around futuristic obstacles.", url: "https://www.crazygames.com/game/space-waves" }
        ];

        function renderCatalog(games) {
            const container = document.getElementById('catalogContainer');
            container.innerHTML = '';

            const grouped = {};
            games.forEach(game => {
                if (!grouped[game.category]) {
                    grouped[game.category] = [];
                }
                grouped[game.category].push(game);
            });

            for (const category in grouped) {
                if (grouped[category].length === 0) continue;

                const section = document.createElement('section');
                section.className = 'category-section';

                const title = document.createElement('h2');
                title.className = 'category-title';
                title.textContent = `${category} (${grouped[category].length})`;
                section.appendChild(title);

                const grid = document.createElement('div');
                grid.className = 'grid';

                grouped[category].forEach(game => {
                    const card = document.createElement('a');
                    card.className = 'card';
                    card.href = game.url;
                    card.target = "_blank";
                    card.rel = "noopener noreferrer";

                    card.innerHTML = `
                        <div>
                            <h3>${game.title}</h3>
                            <p>${game.desc}</p>
                        </div>
                        <div class="card-footer">
                            <span class="badge">Rated 12+</span>
                            <span class="play-btn">Play ${game.title} ↗</span>
                        </div>
                    `;
                    grid.appendChild(card);
                });

                section.appendChild(grid);
                container.appendChild(section);
            }
        }

        function filterGames() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const selectedCategory = document.getElementById('categoryFilter').value;

            const filtered = gamesCatalog.filter(game => {
                const matchesSearch = game.title.toLowerCase().includes(query);
                const matchesCategory = (selectedCategory === "ALL") || (game.category === selectedCategory);
                return matchesSearch && matchesCategory;
            });

            renderCatalog(filtered);
        }

        renderCatalog(gamesCatalog);
    </script>
</body>
</html>
