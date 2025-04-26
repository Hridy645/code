---
# DO NOT TOUCH — Managed by doc writer
ContentId: AD26EFB1-FFC6-4284-BAB8-F3BCB8294728
DateApproved: 04/03/2025

# Summarize the whole topic in less than 300 characters for SEO purpose
MetaDescription: Visual Studio Code has a rich extension API. Learn how to create your own extensions for VS Code.
---

# Extension API

Visual Studio Code is built with extensibility in mind. From the UI to the editing experience, almost every part of VS Code can be customized and enhanced through the Extension API. In fact, many core features of VS Code are built as [extensions](https://github.com/microsoft/vscode/tree/main/extensions) and use the same Extension API.

This documentation describes:

* How to build, run, debug, test, and publish an extension
* How to take advantage of VS Code's rich Extension API
* Where to find [guides](https://code.visualstudio.com/api/extension-guides/overview) and [code samples](https://github.com/microsoft/vscode-extension-samples) to help get you started
* Following our [UX guidelines](/api/ux-guidelines/overview) for best practices

Code samples are available at [Microsoft/vscode-extension-samples](https://github.com/microsoft/vscode-extension-samples).

If you are looking for published extensions, head to the [VS Code Extension Marketplace](https://marketplace.visualstudio.com/vscode).

## What can extensions do?

Here are some examples of what you can achieve with the Extension API:

* Change the look of VS Code with a color or file icon theme - [Theming](/api/extension-capabilities/theming)
* Add custom components & views in the UI - [Extending the Workbench](/api/extension-capabilities/extending-workbench)
* Create a Webview to display a custom webpage built with HTML/CSS/JS - [Webview Guide](/api/extension-guides/webview)
* Support a new programming language - [Language Extensions Overview](/api/language-extensions/overview)
* Support debugging a specific runtime - [Debugger Extension Guide](/api/extension-guides/debugger-extension)

If you'd like to have a more comprehensive overview of the Extension API, refer to the [Extension Capabilities Overview](/api/extension-capabilities/overview) page. [Extension Guides Overview](/api/extension-guides/overview) also includes a list of code samples and guides that illustrate various Extension API usage.

## How to build extensions?

Building a good extension can take a lot of time and effort. Here is what each section of the API docs can help you with:

* **Get Started** teaches fundamental concepts for building extensions with the [Hello World](https://github.com/microsoft/vscode-extension-samples/tree/main/helloworld-sample) sample.
* **Extension Capabilities** dissects VS Code's vast API into smaller categories and points you to more detailed topics.
* **Extension Guides** includes guides and code samples that explain specific usages of VS Code Extension API.
* **UX Guidelines** showcases best practices for providing a great user experience in an extension.
* **Language Extensions** illustrates how to add support for a programming language with guides and code samples.
* **Testing and Publishing** includes in-depth guides on various extension development topics, such as [testing](/api/working-with-extensions/testing-extension) and [publishing](/api/working-with-extensions/publishing-extension) extensions.
* **Advanced Topics** explains advanced concepts such as [Extension Host](/api/advanced-topics/extension-host), [Supporting Remote Development and GitHub Codespaces](/api/advanced-topics/remote-extensions), and [Proposed API](/api/advanced-topics/using-proposed-api).
* **References** contains exhaustive references for the [VS Code API](/api/references/vscode-api), [Contribution Points](/api/references/contribution-points), and many other topics.

## What's new?

VS Code updates on a monthly cadence, and that applies to the Extension API as well. New features and APIs become available every month to increase the power and scope of VS Code extensions.

To stay current with the Extension API, you can review the monthly release notes, which have dedicated sections covering:

* [Extension authoring](https://code.visualstudio.com/updates#_extension-authoring) - Learn what new extension APIs are available in the latest release.
* [Proposed extension APIs](https://code.visualstudio.com/updates#_proposed-extension-apis) - Review and give feedback on upcoming proposed APIs.

## Looking for help

If you have questions for extension development, try asking on:

* [VS Code Discussions](https://github.com/microsoft/vscode-discussions): GitHub community to discuss VS Code's extension platform, ask questions, help other members of the community, and get answers.
* [Stack Overflow](https://stackoverflow.com/questions/tagged/vscode-extensions): There are [thousands of questions](https://stackoverflow.com/questions/tagged/vscode-extensions) tagged `vscode-extensions`, and over half of them already have answers. Search for your issue, ask questions, or help your fellow developers by answering VS Code extension development questions!
* [VS Code Dev Slack](https://vscode-dev-community.slack.com): Public chatroom for extension developers. VS Code team members often join in the conversations.

To provide feedback on the documentation, create new issues at [Microsoft/vscode-docs](https://github.com/microsoft/vscode-docs/issues).
If you have extension questions that you cannot find an answer for, or issues with the VS Code Extension API, please open new issues at [Microsoft/vscode](https://github.com/microsoft/vscode/issues).
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Country Explorer</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f5f5f5;
            color: #333;
            line-height: 1.6;
        }

        .navbar {
            background-color: #2c3e50;
            color: white;
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .logo {
            font-size: 1.5rem;
            font-weight: bold;
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            margin-left: 1.5rem;
            transition: color 0.3s;
        }

        .nav-links a:hover {
            color: #3498db;
        }

        .container {
            max-width: 1200px;
            margin: 2rem auto;
            padding: 0 1rem;
        }

        .search-container {
            text-align: center;
            margin-bottom: 2rem;
        }

        .search-container h1 {
            margin-bottom: 1rem;
            color: #2c3e50;
        }

        .search-box {
            display: flex;
            justify-content: center;
            max-width: 600px;
            margin: 0 auto;
        }

        #country-input {
            width: 70%;
            padding: 0.8rem;
            border: 1px solid #ddd;
            border-radius: 4px 0 0 4px;
            font-size: 1rem;
            outline: none;
        }

        #search-btn {
            padding: 0.8rem 1.5rem;
            background-color: #3498db;
            color: white;
            border: none;
            border-radius: 0 4px 4px 0;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s;
        }

        #search-btn:hover {
            background-color: #2980b9;
        }

        .results-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1.5rem;
            margin-top: 2rem;
        }

        .country-card {
            background-color: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s;
        }

        .country-card:hover {
            transform: translateY(-5px);
        }

        .card-header {
            background-color: #3498db;
            color: white;
            padding: 1rem;
            text-align: center;
        }

        .card-body {
            padding: 1.5rem;
        }

        .card-body ul {
            list-style-type: none;
        }

        .card-body li {
            margin-bottom: 0.5rem;
            display: flex;
            align-items: center;
        }

        .card-body li i {
            margin-right: 0.5rem;
            color: #3498db;
        }

        .details-btn {
            display: block;
            width: 100%;
            padding: 0.8rem;
            background-color: #2c3e50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
            margin-top: 1rem;
            transition: background-color 0.3s;
        }

        .details-btn:hover {
            background-color: #1a252f;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1000;
            overflow-y: auto;
        }

        .modal-content {
            background-color: white;
            margin: 3rem auto;
            padding: 2rem;
            border-radius: 8px;
            max-width: 800px;
            width: 90%;
            position: relative;
        }

        .close-btn {
            position: absolute;
            top: 1rem;
            right: 1rem;
            font-size: 1.5rem;
            cursor: pointer;
            color: #777;
        }

        .modal-header {
            display: flex;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .country-flag {
            width: 100px;
            height: auto;
            margin-right: 1.5rem;
            border: 1px solid #ddd;
        }

        .modal-body {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1.5rem;
        }

        .weather-info {
            margin-top: 1.5rem;
            padding-top: 1.5rem;
            border-top: 1px solid #eee;
            grid-column: 1 / -1;
        }

        .footer {
            background-color: #2c3e50;
            color: white;
            text-align: center;
            padding: 1.5rem;
            margin-top: 2rem;
        }

        .loading {
            text-align: center;
            margin: 2rem 0;
            display: none;
        }

        .spinner {
            border: 4px solid rgba(0, 0, 0, 0.1);
            border-radius: 50%;
            border-top: 4px solid #3498db;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        @media (max-width: 768px) {
            .modal-body {
                grid-template-columns: 1fr;
            }

            .navbar {
                flex-direction: column;
                padding: 1rem;
            }

            .nav-links {
                margin-top: 1rem;
            }

            .nav-links a {
                margin: 0 0.5rem;
            }
        }
    </style>
</head>
<body>
    <nav class="navbar">
        <div class="logo">Country Explorer</div>
        <div class="nav-links">
            <a href="#">Home</a>
            <a href="#">About</a>
            <a href="#">Contact</a>
        </div>
    </nav>

    <div class="container">
        <div class="search-container">
            <h1>Explore Countries Around the World</h1>
            <div class="search-box">
                <input type="text" id="country-input" placeholder="Enter country name...">
                <button id="search-btn">Search</button>
            </div>
        </div>

        <div class="loading">
            <div class="spinner"></div>
            <p>Loading data...</p>
        </div>

        <div class="results-container" id="results-container">
            <!-- Results will be displayed here -->
        </div>
    </div>

    <div class="modal" id="modal">
        <div class="modal-content">
            <span class="close-btn" id="close-modal">&times;</span>
            <div class="modal-header">
                <img src="" alt="Country Flag" class="country-flag" id="modal-flag">
                <h2 id="modal-title">Country Details</h2>
            </div>
            <div class="modal-body" id="modal-body">
                <!-- Detailed information will be displayed here -->
            </div>
            <div class="weather-info" id="weather-info">
                <!-- Weather information will be displayed here -->
            </div>
        </div>
    </div>

    <footer class="footer">
        <p>&copy; 2023 Country Explorer. All rights reserved.</p>
        <p>Created for Educational Purposes</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const searchBtn = document.getElementById('search-btn');
            const countryInput = document.getElementById('country-input');
            const resultsContainer = document.getElementById('results-container');
            const loading = document.querySelector('.loading');
            const modal = document.getElementById('modal');
            const closeModal = document.getElementById('close-modal');
            const modalTitle = document.getElementById('modal-title');
            const modalFlag = document.getElementById('modal-flag');
            const modalBody = document.getElementById('modal-body');
            const weatherInfo = document.getElementById('weather-info');

            // Search for countries
            searchBtn.addEventListener('click', searchCountries);
            countryInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    searchCountries();
                }
            });

            // Close modal
            closeModal.addEventListener('click', function() {
                modal.style.display = 'none';
            });

            // Close modal when clicking outside
            window.addEventListener('click', function(e) {
                if (e.target === modal) {
                    modal.style.display = 'none';
                }
            });

            async function searchCountries() {
                const countryName = countryInput.value.trim();
                if (!countryName) return;

                loading.style.display = 'block';
                resultsContainer.innerHTML = '';

                try {
                    const response = await fetch(https://restcountries.com/v3.1/name/${countryName});
                    if (!response.ok) throw new Error('Country not found');

                    const countries = await response.json();
                    displayCountries(countries);
                } catch (error) {
                    resultsContainer.innerHTML = <p class="error">${error.message}. Please try another country.</p>;
                } finally {
                    loading.style.display = 'none';
                }
            }

            function displayCountries(countries) {
                resultsContainer.innerHTML = '';

                countries.forEach(country => {
                    const countryCard = document.createElement('div');
                    countryCard.className = 'country-card';

                    countryCard.innerHTML = `
                        <div class="card-header">
                            <h3>${country.name.common}</h3>
                        </div>
                        <div class="card-body">
                            <ul>
                                <li><i class="fas fa-globe"></i> <strong>Region:</strong> ${country.region}</li>
                                <li><i class="fas fa-users"></i> <strong>Population:</strong> ${country.population.toLocaleString()}</li>
                                <li><i class="fas fa-city"></i> <strong>Capital:</strong> ${country.capital ? country.capital[0] : 'N/A'}</li>
                                <li><i class="fas fa-money-bill-wave"></i> <strong>Currency:</strong> ${country.currencies ? Object.values(country.currencies)[0].name : 'N/A'}</li>
                            </ul>
                            <button class="details-btn" data-country="${country.name.common}">More Details</button>
                        </div>
                    `;

                    resultsContainer.appendChild(countryCard);
                });

                // Add event listeners to all details buttons
                document.querySelectorAll('.details-btn').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const countryName = this.getAttribute('data-country');
                        showCountryDetails(countryName);
                    });
                });
            }

            async function showCountryDetails(countryName) {
                loading.style.display = 'block';
                modal.style.display = 'none';

                try {
                    // Get country details
                    const response = await fetch(https://restcountries.com/v3.1/name/${countryName}?fullText=true);
                    if (!response.ok) throw new Error('Country details not found');

                    const [country] = await response.json();

                    // Display basic details in modal
                    modalTitle.textContent = country.name.common;
                    modalFlag.src = country.flags.png;
                    modalFlag.alt = Flag of ${country.name.common};

                    // Prepare modal body content
                    modalBody.innerHTML = `
                        <div>
                            <h4>Basic Information</h4>
                            <ul>
                                <li><i class="fas fa-globe-americas"></i> <strong>Official Name:</strong> ${country.name.official}</li>
                                <li><i class="fas fa-map-marked-alt"></i> <strong>Continent:</strong> ${country.region}</li>
                                <li><i class="fas fa-subscript"></i> <strong>Subregion:</strong> ${country.subregion || 'N/A'}</li>
                                <li><i class="fas fa-map"></i> <strong>Area:</strong> ${country.area.toLocaleString()} km²</li>
                            </ul>
                        </div>
                        <div>
                            <h4>Demographics</h4>
                            <ul>
                                <li><i class="fas fa-users"></i> <strong>Population:</strong> ${country.population.toLocaleString()}</li>
                                <li><i class="fas fa-language"></i> <strong>Languages:</strong> ${country.languages ? Object.values(country.languages).join(', ') : 'N/A'}</li>
                                <li><i class="fas fa-coins"></i> <strong>Currencies:</strong> ${country.currencies ? Object.values(country.currencies).map(c => ${c.name} (${c.symbol || 'N/A'})).join(', ') : 'N/A'}</li>
                                <li><i class="fas fa-clock"></i> <strong>Timezones:</strong> ${country.timezones.join(', ')}</li>
                            </ul>
                        </div>
                    `;

                    // Get weather data (using OpenWeatherMap API as an example)
                    // Note: In a real application, you would need to sign up for an API key
                    const capital = country.capital ? country.capital[0] : null;
                    if (capital) {
                        try {
                            // This is a mock implementation since we don't have a real API key
                            // In a real app, you would make an actual API call to a weather service
                            weatherInfo.innerHTML = `
                                <h4>Weather in ${capital}</h4>
                                <p><i class="fas fa-temperature-high"></i> <strong>Temperature:</strong> 25°C (simulated data)</p>
                                <p><i class="fas fa-cloud"></i> <strong>Conditions:</strong> Partly Cloudy (simulated data)</p>
                                <p><i class="fas fa-wind"></i> <strong>Wind:</strong> 12 km/h (simulated data)</p>
                                <p class="note">Note: This is simulated weather data. To implement real weather data, sign up for a weather API service.</p>
                            `;
                        } catch (error) {
                            weatherInfo.innerHTML = <p>Could not load weather data: ${error.message}</p>;
                        }
                    } else {
                        weatherInfo.innerHTML = '<p>No capital city available for weather data.</p>';
                    }

                    modal.style.display = 'block';
                } catch (error) {
                    alert(Error: ${error.message});
                } finally {
                    loading.style.display = 'none';
                }
            }
        });
    </script>
</body>
</html>