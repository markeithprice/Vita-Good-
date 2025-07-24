<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vita Good - Vitamin & Activity Planner</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            background-color: #111827; /* Dark Gray - Tailwind gray-900 */
            font-family: 'Inter', sans-serif;
            color: #D1D5DB; /* Light Gray - Tailwind gray-300 */
        }
        .menu-item {
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .menu-item:hover, .menu-item.active {
            color: #818CF8; /* Light Indigo */
            border-bottom: 2px solid #818CF8;
        }
        #health-hub-menu.active {
             color: #818CF8; /* Light Indigo */
        }
        .btn-primary {
            background-color: #4F46E5;
            color: white;
            transition: background-color 0.3s ease;
        }
        .btn-primary:hover {
            background-color: #6366F1;
        }
        .btn-secondary {
            background-color: #EC4899; /* Pink */
            color: white;
            transition: background-color 0.3s ease;
        }
        .btn-secondary:hover {
            background-color: #F472B6;
        }
        .card {
            background-color: #1F2937; /* Lighter Dark Gray - Tailwind gray-800 */
            border-radius: 1rem;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            transition: all 0.3s ease;
        }
        .card.interactive-card {
             cursor: pointer;
        }
        .card.interactive-card:hover {
            transform: translateY(-5px) scale(1.02);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        .details-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-in-out;
        }
        .card.open .details-content {
            max-height: 2000px; /* Adjust as needed */
        }
        .category-heading {
            grid-column: 1 / -1; /* Span full width */
            color: #F9FAFB; /* Tailwind gray-50 */
            border-bottom: 2px solid #374151; /* Tailwind gray-700 */
            padding-bottom: 0.5rem;
            margin-top: 2rem;
            margin-bottom: 1rem;
        }
        /* Custom colors for text remain vibrant */
        .text-vitamin-a { color: #F59E0B; } /* Amber */
        .text-vitamin-c { color: #F97316; } /* Orange */
        .text-vitamin-d { color: #FBBF24; } /* Yellow */
        .text-vitamin-e { color: #84CC16; } /* Lime */
        .text-vitamin-k { color: #22C55E; } /* Green */
        .text-b-vitamins { color: #3B82F6; } /* Blue */
        .text-calcium { color: #A78BFA; } /* Violet */
        .text-iron { color: #EF4444; } /* Red */
        .text-magnesium { color: #14B8A6; } /* Teal */
        .text-zinc { color: #64748B; } /* Slate */
        .text-amino-acids { color: #EC4899; } /* Pink */
        .text-enzymes { color: #A855F7; } /* Purple */

        /* Custom colors for pills */
        .bg-vitamin-a { color: white; background-color: #F59E0B; }
        .bg-vitamin-c { color: white; background-color: #F97316; }
        .bg-vitamin-d { color: white; background-color: #FBBF24; }
        .bg-vitamin-e { color: white; background-color: #84CC16; }
        .bg-vitamin-k { color: white; background-color: #22C55E; }
        .bg-b-vitamins { color: white; background-color: #3B82F6; }
        .bg-minerals { color: white; background-color: #A78BFA; }
        .bg-amino-acids { color: white; background-color: #EC4899; }
        .bg-enzymes { color: white; background-color: #A855F7; }
        .bg-other { color: white; background-color: #64748B; }

        /* Loading Spinner */
        .loader {
            border: 4px solid #374151; /* gray-700 */
            border-radius: 50%;
            border-top: 4px solid #818CF8; /* light indigo */
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .dropdown-menu {
            display: none;
        }
        .dropdown-menu.show {
            display: block;
        }
    </style>
</head>
<body class="antialiased">

    <!-- Header and Menu -->
    <header class="bg-[#1f2937] shadow-lg sticky top-0 z-50">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex flex-col sm:flex-row items-center justify-between py-4">
                <div class="text-center sm:text-left mb-4 sm:mb-0">
                    <h1 class="text-3xl font-bold text-white">Vita Good</h1>
                    <p class="text-sm text-gray-400 mt-1">By Heart Motivation</p>
                </div>
                <nav class="flex flex-wrap justify-center items-center space-x-2 sm:space-x-4 text-sm md:text-base">
                    <span id="menu-calculator" class="menu-item active px-2 py-2">Nutrition Calc</span>
                    <span id="menu-activity" class="menu-item px-2 py-2">Activity Planner</span>
                    <div class="relative dropdown">
                        <button id="health-hub-menu" class="menu-item px-2 py-2 flex items-center">
                            Health Hub
                            <svg class="w-4 h-4 ml-1" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path></svg>
                        </button>
                        <div id="health-hub-dropdown" class="dropdown-menu absolute right-0 mt-2 w-48 bg-gray-800 rounded-md shadow-lg z-50 border border-gray-700">
                            <a href="#" id="menu-meals" class="block px-4 py-2 text-gray-300 hover:bg-gray-700">Meal Ideas</a>
                            <a href="#" id="menu-foods" class="block px-4 py-2 text-gray-300 hover:bg-gray-700">Food List</a>
                            <a href="#" id="menu-info" class="block px-4 py-2 text-gray-300 hover:bg-gray-700">Nutrient Info</a>
                            <a href="#" id="menu-fitness" class="block px-4 py-2 text-gray-300 hover:bg-gray-700">Fitness Hub</a>
                        </div>
                    </div>
                </nav>
            </div>
        </div>
    </header>

    <!-- Accessibility Controls -->
    <div id="accessibility-controls" class="bg-gray-800 border-b border-gray-700 py-2 sticky top-[109px] sm:top-[77px] z-40">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8 flex justify-center items-center space-x-4">
            <button id="speak-btn" class="flex items-center space-x-2 px-3 py-1.5 rounded-lg bg-gray-700 border border-gray-600 text-gray-300 hover:bg-gray-600 transition-colors duration-200" title="Read Aloud">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M19.114 5.636a9 9 0 010 12.728M16.463 8.288a5 5 0 010 7.424M6.75 8.25l4.72-4.72a.75.75 0 011.28.53v15.88a.75.75 0 01-1.28.53l-4.72-4.72H4.51c-.88 0-1.704-.507-1.938-1.354A9.01 9.01 0 012.25 12c0-.83.112-1.633.322-2.396C2.806 8.756 3.63 8.25 4.51 8.25H6.75z" />
                </svg>
                <span class="text-sm font-medium">Speak</span>
            </button>
            <div class="flex items-center space-x-1 bg-gray-700 border border-gray-600 rounded-lg p-0.5">
                 <span class="text-sm font-medium text-gray-400 pl-2 pr-1">Zoom:</span>
                <button id="zoom-out-btn" class="w-8 h-8 flex items-center justify-center text-lg font-bold rounded-md text-gray-300 hover:bg-gray-600 transition-colors duration-200" title="Zoom Out">-</button>
                <button id="zoom-in-btn" class="w-8 h-8 flex items-center justify-center text-lg font-bold rounded-md text-gray-300 hover:bg-gray-600 transition-colors duration-200" title="Zoom In">+</button>
            </div>
        </div>
    </div>

    <!-- Main Content -->
    <main id="main-content" class="container mx-auto p-4 sm:p-6 lg:p-8">
        
        <!-- Vitamin Calculator Section -->
        <section id="calculator-section">
            <div class="text-center mb-8">
                <h2 class="text-3xl font-bold text-white">Essential Nutrition Calculator</h2>
                <p class="text-gray-400 mt-2">Calculate your estimated daily vitamin needs based on your profile.</p>
            </div>
            <div class="max-w-2xl mx-auto card p-6 sm:p-8">
                <form id="vitamin-calculator-form" class="space-y-6">
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                        <div>
                            <label for="nutrition-age" class="block text-sm font-medium text-gray-300">Age</label>
                            <input type="number" id="nutrition-age" name="nutrition-age" required class="mt-1 block w-full px-3 py-2 bg-gray-700 border border-gray-600 text-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="e.g., 35">
                        </div>
                        <div>
                            <label for="nutrition-gender" class="block text-sm font-medium text-gray-300">Gender</label>
                            <select id="nutrition-gender" name="nutrition-gender" class="mt-1 block w-full pl-3 pr-10 py-2 bg-gray-700 border-gray-600 text-white sm:text-sm rounded-md">
                                <option value="female">Female</option>
                                <option value="male">Male</option>
                                <option value="prefer_not_to_say">Prefer not to say</option>
                                <option value="other">Other</option>
                            </select>
                        </div>
                    </div>
                     <div id="nutrition-gender-other-container" class="hidden">
                        <label for="nutrition-gender-other" class="block text-sm font-medium text-gray-300">Please Specify</label>
                        <input type="text" id="nutrition-gender-other" name="nutrition-gender-other" class="mt-1 block w-full px-3 py-2 bg-gray-700 border border-gray-600 text-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="How do you identify?">
                    </div>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                        <div>
                            <label for="weight" class="block text-sm font-medium text-gray-300">Weight (kg)</label>
                            <input type="number" id="weight" name="weight" required class="mt-1 block w-full px-3 py-2 bg-gray-700 border border-gray-600 text-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="e.g., 70">
                        </div>
                        <div>
                             <label for="height" class="block text-sm font-medium text-gray-300">Height</label>
                             <div class="mt-1 flex rounded-md shadow-sm">
                                <input type="number" id="height" name="height" required class="block w-full px-3 py-2 bg-gray-700 border border-gray-600 text-white rounded-none rounded-l-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="e.g., 175">
                                <select id="height-unit" class="px-4 py-2 bg-gray-600 border-t border-b border-r border-gray-600 text-white rounded-r-md">
                                    <option value="cm">cm</option>
                                    <option value="in">in</option>
                                </select>
                             </div>
                        </div>
                    </div>
                    <div>
                        <label for="activity-level" class="block text-sm font-medium text-gray-300">Nutritional Activity Level</label>
                        <select id="activity-level" name="activity-level" class="mt-1 block w-full pl-3 pr-10 py-2 bg-gray-700 border-gray-600 text-white sm:text-sm rounded-md">
                            <option value="1.2">Sedentary (little or no exercise)</option>
                            <option value="1.375">Lightly active (light exercise/sports 1-3 days/week)</option>
                            <option value="1.55">Moderately active (moderate exercise/sports 3-5 days/week)</option>
                            <option value="1.725">Very active (hard exercise/sports 6-7 days a week)</option>
                            <option value="1.9">Extra active (very hard exercise/sports & physical job)</option>
                        </select>
                    </div>
                    <div class="text-center">
                        <button type="submit" class="btn-primary font-bold py-2 px-6 rounded-lg shadow-lg transform hover:scale-105 transition-transform duration-300">
                            Calculate My Needs
                        </button>
                    </div>
                </form>
            </div>
            <div id="results-section" class="mt-10 hidden">
                <h3 class="text-2xl font-bold text-center text-white mb-6">Your Estimated Daily Needs</h3>
                <div id="results-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6"></div>
                <div id="gemini-cta-container" class="text-center mt-8 hidden">
                    <button id="generate-meal-btn" class="btn-secondary font-bold py-3 px-8 rounded-lg shadow-lg transform hover:scale-105 transition-transform duration-300">
                        ✨ Get a Meal Idea
                    </button>
                </div>
            </div>
            <div id="gemini-results-section" class="mt-10 hidden">
                 <div class="max-w-2xl mx-auto card p-6 sm:p-8">
                    <h3 class="text-2xl font-bold text-center text-white mb-4">✨ Your AI-Generated Meal Idea</h3>
                    <div id="gemini-loading" class="flex justify-center items-center py-8">
                        <div class="loader"></div>
                        <p class="ml-4 text-gray-400">Generating your meal...</p>
                    </div>
                    <div id="gemini-content" class="prose prose-invert max-w-none text-gray-300"></div>
                 </div>
            </div>
        </section>

        <!-- Activity Planner Section -->
        <section id="activity-section" class="hidden">
            <div class="text-center mb-8">
                <h2 class="text-3xl font-bold text-white">Weekly Activity Planner</h2>
                <p class="text-gray-400 mt-2">Get a science-based recommendation for your weekly physical activity.</p>
            </div>
            <div class="max-w-2xl mx-auto card p-6 sm:p-8">
                <form id="activity-calculator-form" class="space-y-6">
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                        <div>
                            <label for="activity-age" class="block text-sm font-medium text-gray-300">Age</label>
                            <input type="number" id="activity-age" name="activity-age" required class="mt-1 block w-full px-3 py-2 bg-gray-700 border border-gray-600 text-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="e.g., 35">
                        </div>
                        <div>
                            <label for="activity-gender" class="block text-sm font-medium text-gray-300">Gender</label>
                            <select id="activity-gender" name="activity-gender" class="mt-1 block w-full pl-3 pr-10 py-2 bg-gray-700 border-gray-600 text-white sm:text-sm rounded-md">
                                <option value="female">Female</option>
                                <option value="male">Male</option>
                                <option value="other">Other</option>
                            </select>
                        </div>
                    </div>
                    <div id="activity-gender-other-container" class="hidden">
                        <label for="activity-gender-other" class="block text-sm font-medium text-gray-300">Please Specify</label>
                        <input type="text" id="activity-gender-other" name="activity-gender-other" class="mt-1 block w-full px-3 py-2 bg-gray-700 border border-gray-600 text-white rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" placeholder="How do you identify?">
                    </div>
                     <div class="text-center">
                        <button type="submit" class="btn-primary font-bold py-2 px-6 rounded-lg shadow-lg transform hover:scale-105 transition-transform duration-300">
                            Plan My Activity
                        </button>
                    </div>
                </form>
            </div>
            <div id="activity-results-section" class="mt-10 hidden">
                <div class="max-w-2xl mx-auto card p-6 sm:p-8 text-center">
                    <h3 class="text-2xl font-bold text-white mb-4">Your Weekly Activity Goal</h3>
                    <p class="text-gray-400 mb-6">Based on guidelines for adults, here is your suggested weekly target:</p>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 text-left">
                        <div class="bg-gray-700 p-4 rounded-lg">
                            <h4 class="font-bold text-indigo-300">Moderate-Intensity Activity</h4>
                            <p id="moderate-activity-goal" class="text-3xl font-bold text-indigo-400 mt-2">150-300 mins</p>
                            <p class="text-sm text-gray-400">e.g., Brisk Walking, Cycling, Swimming</p>
                        </div>
                        <div class="bg-gray-700 p-4 rounded-lg">
                            <h4 class="font-bold text-pink-300">Vigorous-Intensity Activity</h4>
                             <p id="vigorous-activity-goal" class="text-3xl font-bold text-pink-400 mt-2">75-150 mins</p>
                             <p class="text-sm text-gray-400">e.g., Running, HIIT, Sports</p>
                        </div>
                    </div>
                    <p class="mt-6 text-sm text-gray-500">You can also do a combination of both. Plus, aim for muscle-strengthening activities on 2 or more days a week.</p>
                </div>
            </div>
        </section>

        <!-- Meal Ideas Section -->
        <section id="meals-section" class="hidden">
            <div class="text-center mb-8">
                <h2 class="text-3xl font-bold text-white">Healthy Meal Ideas</h2>
                <p class="text-gray-400 mt-2">Discover a variety of healthy, gluten-conscious recipes. Click any meal to see the steps.</p>
            </div>
            <div id="meal-ideas-grid" class="space-y-8"></div>
        </section>

        <!-- Food List Section -->
        <section id="food-list-section" class="hidden">
             <div class="text-center mb-8">
                <h2 class="text-3xl font-bold text-white">Nutrient-Rich Foods Database</h2>
                <p class="text-gray-400 mt-2">Search for a food or click to see its detailed nutritional facts (per 100g serving).</p>
            </div>
            <div class="mb-8 max-w-xl mx-auto">
                <input type="text" id="food-search" placeholder="🔍 Search for a food..." class="w-full px-4 py-3 bg-gray-700 border border-gray-600 text-white rounded-full shadow-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 placeholder-gray-400">
            </div>
            <div id="food-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6"></div>
        </section>

        <!-- Nutrient Info Section -->
        <section id="info-section" class="hidden">
            <div class="text-center mb-8">
                <h2 class="text-3xl font-bold text-white">Learn About Your Nutrients</h2>
                <p class="text-gray-400 mt-2">Search for a nutrient to learn about its function.</p>
            </div>
            <div class="mb-8 max-w-xl mx-auto">
                <input type="text" id="nutrient-search" placeholder="🔍 Search for a vitamin, amino acid, or enzyme..." class="w-full px-4 py-3 bg-gray-700 border border-gray-600 text-white rounded-full shadow-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 placeholder-gray-400">
            </div>
            <div id="info-grid" class="space-y-8"></div>
        </section>

        <!-- Fitness Hub Section -->
        <section id="fitness-section" class="hidden">
            <div class="text-center mb-8">
                <h2 class="text-3xl font-bold text-white">Fitness Hub</h2>
                <p class="text-gray-400 mt-2">Explore exercises and find a workout routine that's right for you.</p>
            </div>
            
            <!-- Fitness Sub-navigation -->
            <div class="flex justify-center border-b border-gray-700 mb-8">
                <button id="fitness-tab-exercises" class="py-2 px-6 text-lg font-semibold border-b-2 border-indigo-400 text-indigo-400">Exercises</button>
                <button id="fitness-tab-routines" class="py-2 px-6 text-lg font-semibold text-gray-500">Routines</button>
            </div>

            <!-- Exercises Content -->
            <div id="fitness-exercises-content">
                <div class="mb-8 max-w-xl mx-auto">
                    <input type="text" id="exercise-search" placeholder="🔍 Search for an exercise..." class="w-full px-4 py-3 bg-gray-700 border border-gray-600 text-white rounded-full shadow-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 placeholder-gray-400">
                </div>
                <div id="exercise-grid" class="space-y-8"></div>
            </div>

            <!-- Routines Content -->
            <div id="fitness-routines-content" class="hidden">
                <div id="routines-grid" class="space-y-8"></div>
            </div>
        </section>

    </main>
    
    <!-- Footer -->
    <footer class="text-center py-6 mt-10 border-t border-gray-700">
        <p class="text-gray-400">&copy; 2025 Vita Good by Heart Motivation. All rights reserved.</p>
        <p class="text-xs text-gray-500 mt-2">Disclaimer: This calculator provides estimates and is not a substitute for professional medical advice. Consult a healthcare provider for personalized recommendations. AI-generated content may be inaccurate. Nutritional data is approximate. Calorie burn estimates are for a ~155lb person and vary greatly.</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // --- DOM Elements ---
            const mainContent = document.getElementById('main-content');
            const menuItems = {
                calculator: document.getElementById('menu-calculator'),
                activity: document.getElementById('menu-activity'),
                meals: document.getElementById('menu-meals'),
                foods: document.getElementById('menu-foods'),
                info: document.getElementById('menu-info'),
                fitness: document.getElementById('menu-fitness'),
            };
            const sections = {
                calculator: document.getElementById('calculator-section'),
                activity: document.getElementById('activity-section'),
                meals: document.getElementById('meals-section'),
                foods: document.getElementById('food-list-section'),
                info: document.getElementById('info-section'),
                fitness: document.getElementById('fitness-section'),
            };
            const healthHubMenu = document.getElementById('health-hub-menu');
            const healthHubDropdown = document.getElementById('health-hub-dropdown');
            const vitaminForm = document.getElementById('vitamin-calculator-form');
            const nutritionGenderSelect = document.getElementById('nutrition-gender');
            const nutritionGenderOtherContainer = document.getElementById('nutrition-gender-other-container');
            const resultsSection = document.getElementById('results-section');
            const resultsGrid = document.getElementById('results-grid');
            const foodGrid = document.getElementById('food-grid');
            const infoGrid = document.getElementById('info-grid');
            const foodSearchInput = document.getElementById('food-search');
            const nutrientSearchInput = document.getElementById('nutrient-search');
            const geminiCtaContainer = document.getElementById('gemini-cta-container');
            const generateMealBtn = document.getElementById('generate-meal-btn');
            const geminiResultsSection = document.getElementById('gemini-results-section');
            const geminiLoading = document.getElementById('gemini-loading');
            const geminiContent = document.getElementById('gemini-content');
            const activityForm = document.getElementById('activity-calculator-form');
            const activityGenderSelect = document.getElementById('activity-gender');
            const activityGenderOtherContainer = document.getElementById('activity-gender-other-container');
            const activityResultsSection = document.getElementById('activity-results-section');
            const mealIdeasGrid = document.getElementById('meal-ideas-grid');
            const fitnessTabExercises = document.getElementById('fitness-tab-exercises');
            const fitnessTabRoutines = document.getElementById('fitness-tab-routines');
            const fitnessExercisesContent = document.getElementById('fitness-exercises-content');
            const fitnessRoutinesContent = document.getElementById('fitness-routines-content');
            const exerciseGrid = document.getElementById('exercise-grid');
            const routinesGrid = document.getElementById('routines-grid');
            const exerciseSearchInput = document.getElementById('exercise-search');
            
            // --- Zoom and Speech Synthesis ---
            const zoomInBtn = document.getElementById('zoom-in-btn');
            const zoomOutBtn = document.getElementById('zoom-out-btn');
            const speakBtn = document.getElementById('speak-btn');
            let currentZoom = 1;
            const synth = window.speechSynthesis;
            let utterance = null;
            let calculatedNeeds = {};

            // --- DATA OBJECTS (ALL DATA IS INCLUDED HERE) ---
            const vitaminData = {
                'Vitamin A': { base: 800, unit: 'mcg', multiplier: 0.1, color: 'text-vitamin-a' },
                'Vitamin C': { base: 80, unit: 'mg', multiplier: 0.2, color: 'text-vitamin-c' },
                'Vitamin D': { base: 15, unit: 'mcg', multiplier: 0.05, color: 'text-vitamin-d' },
                'Vitamin E': { base: 15, unit: 'mg', multiplier: 0.05, color: 'text-vitamin-e' },
                'Vitamin K': { base: 105, unit: 'mcg', multiplier: 0.1, color: 'text-vitamin-k' },
                'B-Vitamins': { base: 0, unit: 'complex', multiplier: 0, color: 'text-b-vitamins' },
                'Calcium': { base: 1150, unit: 'mg', multiplier: 1, color: 'text-calcium' },
                'Iron': { base: 13, unit: 'mg', multiplier: 0.1, color: 'text-iron' },
                'Magnesium': { base: 365, unit: 'mg', multiplier: 0.5, color: 'text-magnesium' },
                'Zinc': { base: 9.5, unit: 'mg', multiplier: 0.05, color: 'text-zinc' },
                'Amino Acids': { base: 0, unit: 'essential', multiplier: 0, color: 'text-amino-acids' },
                'Enzymes': { base: 0, unit: 'digestive', multiplier: 0, color: 'text-enzymes' },
            };

            const nutrientInfoData = {
                "Vitamins": {
                    "Fat-Soluble": [
                        { name: "Vitamin A", info: "Crucial for vision, immune function, reproduction, and cellular communication. Found in carrots, sweet potatoes, and spinach." },
                        { name: "Vitamin D", info: "Essential for calcium absorption, bone health, and immune function. Synthesized from sunlight; found in fatty fish and fortified milk." },
                        { name: "Vitamin E", info: "Acts as an antioxidant, protecting cells from damage. Found in nuts, seeds, and vegetable oils." },
                        { name: "Vitamin K", info: "Vital for blood clotting and building healthy bones. Abundant in leafy green vegetables like kale and spinach." }
                    ],
                    "Water-Soluble": [
                        { name: "Vitamin C (Ascorbic Acid)", info: "A powerful antioxidant necessary for the growth, development, and repair of all body tissues. Found in citrus fruits, bell peppers, and broccoli." },
                        { name: "Vitamin B1 (Thiamine)", info: "Helps the body convert food into energy. Essential for nerve function. Found in whole grains, pork, and legumes." },
                        { name: "Vitamin B2 (Riboflavin)", info: "Important for energy production, cell function, and fat metabolism. Found in dairy products, eggs, and lean meats." },
                        { name: "Vitamin B3 (Niacin)", info: "Plays a role in converting food into energy and helps the nervous system. Found in poultry, fish, and peanuts." },
                        { name: "Vitamin B5 (Pantothenic Acid)", info: "Necessary for making blood cells and converting food into energy. Found in a wide variety of foods." },
                        { name: "Vitamin B6 (Pyridoxine)", info: "Involved in over 100 enzyme reactions, mainly concerning protein metabolism. Found in chickpeas, salmon, and potatoes." },
                        { name: "Vitamin B7 (Biotin)", info: "Helps metabolize carbohydrates, fats, and proteins. Found in eggs, almonds, and cauliflower." },
                        { name: "Vitamin B9 (Folate)", info: "Crucial for proper cell growth and function, and essential during early pregnancy. Found in leafy greens, beans, and fortified cereals." },
                        { name: "Vitamin B12 (Cobalamin)", info: "Required for the formation of red blood cells and for neurological function. Primarily found in animal products." }
                    ]
                },
                "Amino Acids": {
                    "Essential (Must be obtained from diet)": [
                        { name: "Histidine", info: "Used to develop and maintain healthy tissues, particularly the myelin sheaths that protect nerve cells." },
                        { name: "Isoleucine", info: "One of the three Branched-Chain Amino Acids (BCAAs), important for muscle metabolism and is concentrated in muscle tissues." },
                        { name: "Leucine", info: "A BCAA critical for protein synthesis and muscle repair. It also helps regulate blood sugar levels." },
                        { name: "Lysine", info: "Plays a vital role in protein synthesis, hormone and enzyme production, and the absorption of calcium." },
                        { name: "Methionine", info: "Important for metabolism and detoxification. It's also necessary for tissue growth and the absorption of zinc and selenium." },
                        { name: "Phenylalanine", info: "A precursor for the neurotransmitters tyrosine, dopamine, epinephrine, and norepinephrine." },
                        { name: "Threonine", info: "A principal part of structural proteins such as collagen and elastin, which are important components of the skin and connective tissue." },
                        { name: "Tryptophan", info: "A precursor to serotonin, a neurotransmitter that helps regulate appetite, sleep, and mood." },
                        { name: "Valine", info: "A BCAA that helps stimulate muscle growth and regeneration and is involved in energy production." }
                    ],
                    "Non-Essential (Body can produce)": [
                        { name: "Alanine", info: "Plays a key role in transferring nitrogen from peripheral tissues to the liver." },
                        { name: "Asparagine", info: "Important for the proper function of the nervous system." },
                        { name: "Aspartic Acid", info: "Plays a role in the synthesis of other amino acids and in the citric acid and urea cycles." },
                        { name: "Glutamic Acid", info: "Functions as a powerful excitatory neurotransmitter in the central nervous system." }
                    ],
                    "Conditional (Essential in times of illness/stress)": [
                        { name: "Arginine", info: "Becomes essential in times of stress or illness. It's a precursor for nitric oxide, which helps dilate blood vessels." },
                        { name: "Cysteine", info: "Can be synthesized from methionine. It's a component of the antioxidant glutathione." },
                        { name: "Glutamine", info: "The most abundant amino acid in the blood, it's crucial for immune function and intestinal health." },
                        { name: "Glycine", info: "Acts as a neurotransmitter and is a component of creatine and glutathione." },
                        { name: "Proline", info: "Plays a major role in protein synthesis and the structure of collagen." },
                        { name: "Serine", info: "Important in metabolism and the synthesis of proteins, lipids, and other amino acids." },
                        { name: "Tyrosine", info: "Synthesized from phenylalanine, it's a precursor for several important neurotransmitters and hormones." }
                    ]
                },
                "Enzymes": {
                    "Digestive Enzymes": [
                        { name: "Amylase", info: "Found in saliva and the pancreas. It breaks down complex carbohydrates (starches) into simpler sugars." },
                        { name: "Protease (e.g., Pepsin, Trypsin)", info: "Breaks down proteins into smaller peptides and amino acids. Found in the stomach, pancreas, and small intestine." },
                        { name: "Lipase", info: "Breaks down dietary fats into smaller molecules called fatty acids and glycerol. Produced by the pancreas." },
                        { name: "Lactase", info: "Breaks down lactose, the sugar found in milk and dairy products." },
                        { name: "Sucrase", info: "Breaks down sucrose (table sugar) into glucose and fructose." },
                        { name: "Cellulase", info: "Helps break down cellulose, a type of fiber found in fruits and vegetables. Not produced by humans but found in some foods." }
                    ],
                    "Metabolic Enzymes": [
                        { name: "Catalase", info: "An antioxidant enzyme that catalyzes the decomposition of hydrogen peroxide to water and oxygen, protecting cells from oxidative damage." },
                        { name: "Superoxide Dismutase (SOD)", info: "An important antioxidant defense in nearly all cells exposed to oxygen." },
                        { name: "Coenzyme Q10 (CoQ10)", info: "Acts like a vitamin and an enzyme cofactor, essential for energy production in cells and functions as an antioxidant." }
                    ]
                }
            };
            
            const foodData = {
                "Fruits": [
                    { name: 'Apple', color: 'text-vitamin-c', nutrition: { calories: 52, protein: 0.3, carbs: 13.8, fat: 0.2 }, nutrients: { vitamins: ['C', 'K'], minerals: ['Potassium'], other: ['Fiber', 'Quercetin'] } },
                    { name: 'Apricot', color: 'text-vitamin-a', nutrition: { calories: 48, protein: 1.4, carbs: 11, fat: 0.4 }, nutrients: { vitamins: ['A', 'C', 'E'], minerals: ['Potassium'], other: ['Beta-carotene'] } },
                    { name: 'Avocado', color: 'text-vitamin-e', nutrition: { calories: 160, protein: 2, carbs: 8.5, fat: 14.7 }, nutrients: { vitamins: ['K', 'E', 'C', 'B5', 'B6', 'Folate'], minerals: ['Potassium'], other: ['Fiber', 'Monounsaturated Fats'] } },
                    { name: 'Banana', color: 'text-b-vitamins', nutrition: { calories: 89, protein: 1.1, carbs: 22.8, fat: 0.3 }, nutrients: { vitamins: ['B6', 'C'], minerals: ['Potassium', 'Manganese'], other: ['Fiber'] } },
                    { name: 'Blackberries', color: 'text-vitamin-c', nutrition: { calories: 43, protein: 1.4, carbs: 10, fat: 0.5 }, nutrients: { vitamins: ['C', 'K'], minerals: ['Manganese'], other: ['Anthocyanins'] } },
                    { name: 'Blueberries', color: 'text-vitamin-c', nutrition: { calories: 57, protein: 0.7, carbs: 14.5, fat: 0.3 }, nutrients: { vitamins: ['C', 'K'], minerals: ['Manganese'], other: ['Fiber', 'Antioxidants (Anthocyanins)'] } },
                    { name: 'Cantaloupe', color: 'text-vitamin-a', nutrition: { calories: 34, protein: 0.8, carbs: 8.2, fat: 0.2 }, nutrients: { vitamins: ['A', 'C'], minerals: ['Potassium'], other: ['Beta-carotene'] } },
                    { name: 'Cherries', color: 'text-vitamin-c', nutrition: { calories: 50, protein: 1, carbs: 12, fat: 0.3 }, nutrients: { vitamins: ['C'], minerals: ['Potassium'], other: ['Antioxidants', 'Melatonin'] } },
                    { name: 'Cranberries', color: 'text-vitamin-c', nutrition: { calories: 46, protein: 0.4, carbs: 12.2, fat: 0.1 }, nutrients: { vitamins: ['C', 'E', 'K'], minerals: ['Manganese'], other: ['Proanthocyanidins'] } },
                    { name: 'Dates', color: 'text-b-vitamins', nutrition: { calories: 282, protein: 2.5, carbs: 75, fat: 0.4 }, nutrients: { vitamins: ['B6'], minerals: ['Potassium', 'Magnesium', 'Copper'], other: ['Fiber'] } },
                    { name: 'Figs', color: 'text-vitamin-k', nutrition: { calories: 74, protein: 0.8, carbs: 19, fat: 0.3 }, nutrients: { vitamins: ['K', 'B6'], minerals: ['Potassium', 'Manganese'], enzymes: ['Ficain'] } },
                    { name: 'Grapefruit', color: 'text-vitamin-c', nutrition: { calories: 42, protein: 0.8, carbs: 11, fat: 0.1 }, nutrients: { vitamins: ['A', 'C'], other: ['Fiber', 'Lycopene'] } },
                    { name: 'Grapes', color: 'text-vitamin-c', nutrition: { calories: 69, protein: 0.7, carbs: 18, fat: 0.2 }, nutrients: { vitamins: ['C', 'K'], other: ['Antioxidants', 'Resveratrol'] } },
                    { name: 'Guava', color: 'text-vitamin-c', nutrition: { calories: 68, protein: 2.6, carbs: 14, fat: 1 }, nutrients: { vitamins: ['C', 'A'], minerals: ['Potassium'], other: ['Lycopene'] } },
                    { name: 'Honeydew Melon', color: 'text-vitamin-c', nutrition: { calories: 36, protein: 0.5, carbs: 9, fat: 0.1 }, nutrients: { vitamins: ['C', 'B6'], minerals: ['Potassium'] } },
                    { name: 'Kiwi', color: 'text-vitamin-c', nutrition: { calories: 61, protein: 1.1, carbs: 15, fat: 0.5 }, nutrients: { vitamins: ['C', 'K', 'E'], minerals: ['Potassium'], enzymes: ['Actinidin'], other: ['Fiber'] } },
                    { name: 'Lemon', color: 'text-vitamin-c', nutrition: { calories: 29, protein: 1.1, carbs: 9, fat: 0.3 }, nutrients: { vitamins: ['C'], other: ['Flavonoids', 'Citric Acid'] } },
                    { name: 'Lime', color: 'text-vitamin-c', nutrition: { calories: 30, protein: 0.7, carbs: 11, fat: 0.2 }, nutrients: { vitamins: ['C'], other: ['Flavonoids'] } },
                    { name: 'Lychee', color: 'text-vitamin-c', nutrition: { calories: 66, protein: 0.8, carbs: 17, fat: 0.4 }, nutrients: { vitamins: ['C'], minerals: ['Copper', 'Potassium'] } },
                    { name: 'Mango', color: 'text-vitamin-a', nutrition: { calories: 60, protein: 0.8, carbs: 15, fat: 0.4 }, nutrients: { vitamins: ['A', 'C'], enzymes: ['Amylase'], other: ['Beta-carotene'] } },
                    { name: 'Nectarine', color: 'text-vitamin-c', nutrition: { calories: 44, protein: 1.1, carbs: 11, fat: 0.3 }, nutrients: { vitamins: ['C', 'A', 'B3'], minerals: ['Potassium'] } },
                    { name: 'Olives', color: 'text-vitamin-e', nutrition: { calories: 115, protein: 0.8, carbs: 6, fat: 11 }, nutrients: { vitamins: ['E'], minerals: ['Iron', 'Copper', 'Calcium'], other: ['Oleuropein'] } },
                    { name: 'Orange', color: 'text-vitamin-c', nutrition: { calories: 47, protein: 0.9, carbs: 12, fat: 0.1 }, nutrients: { vitamins: ['C', 'B1', 'Folate'], other: ['Fiber', 'Flavonoids'] } },
                    { name: 'Papaya', color: 'text-enzymes', nutrition: { calories: 43, protein: 0.5, carbs: 11, fat: 0.3 }, nutrients: { vitamins: ['C', 'A'], enzymes: ['Papain'], other: ['Antioxidants'] } },
                    { name: 'Passion Fruit', color: 'text-vitamin-a', nutrition: { calories: 97, protein: 2.2, carbs: 23, fat: 0.7 }, nutrients: { vitamins: ['A', 'C'], minerals: ['Potassium', 'Iron'], other: ['Fiber'] } },
                    { name: 'Peach', color: 'text-vitamin-c', nutrition: { calories: 39, protein: 0.9, carbs: 10, fat: 0.3 }, nutrients: { vitamins: ['C', 'A'], minerals: ['Potassium'] } },
                    { name: 'Pear', color: 'text-vitamin-c', nutrition: { calories: 57, protein: 0.4, carbs: 15, fat: 0.1 }, nutrients: { vitamins: ['C', 'K'], minerals: ['Copper'], other: ['Fiber'] } },
                    { name: 'Persimmon', color: 'text-vitamin-a', nutrition: { calories: 70, protein: 0.6, carbs: 19, fat: 0.2 }, nutrients: { vitamins: ['A', 'C'], minerals: ['Manganese'], other: ['Antioxidants'] } },
                    { name: 'Pineapple', color: 'text-enzymes', nutrition: { calories: 50, protein: 0.5, carbs: 13, fat: 0.1 }, nutrients: { vitamins: ['C', 'B1'], minerals: ['Manganese'], enzymes: ['Bromelain'], other: ['Antioxidants'] } },
                    { name: 'Plum', color: 'text-vitamin-c', nutrition: { calories: 46, protein: 0.7, carbs: 11, fat: 0.3 }, nutrients: { vitamins: ['C', 'K', 'A'], minerals: ['Potassium'] } },
                    { name: 'Pomegranate', color: 'text-vitamin-c', nutrition: { calories: 83, protein: 1.7, carbs: 19, fat: 1.2 }, nutrients: { vitamins: ['C', 'K'], minerals: ['Potassium'], other: ['Punicalagins'] } },
                    { name: 'Raspberries', color: 'text-vitamin-c', nutrition: { calories: 52, protein: 1.2, carbs: 12, fat: 0.7 }, nutrients: { vitamins: ['C', 'K'], minerals: ['Manganese'], other: ['Ellagic Acid'] } },
                    { name: 'Strawberries', color: 'text-vitamin-c', nutrition: { calories: 32, protein: 0.7, carbs: 8, fat: 0.3 }, nutrients: { vitamins: ['C'], minerals: ['Manganese'], other: ['Antioxidants'] } },
                    { name: 'Watermelon', color: 'text-vitamin-a', nutrition: { calories: 30, protein: 0.6, carbs: 8, fat: 0.2 }, nutrients: { vitamins: ['C', 'A'], other: ['Lycopene', 'Citrulline'] } },
                ],
                "Vegetables": [
                    { name: 'Artichoke', color: 'text-vitamin-k', nutrition: { calories: 47, protein: 3.3, carbs: 11, fat: 0.2 }, nutrients: { vitamins: ['K', 'Folate', 'C'], minerals: ['Magnesium'], other: ['Cynarin'] } },
                    { name: 'Arugula', color: 'text-vitamin-k', nutrition: { calories: 25, protein: 2.6, carbs: 3.7, fat: 0.7 }, nutrients: { vitamins: ['K', 'A', 'C'], minerals: ['Calcium'] } },
                    { name: 'Asparagus', color: 'text-vitamin-k', nutrition: { calories: 20, protein: 2.2, carbs: 3.9, fat: 0.1 }, nutrients: { vitamins: ['K', 'A', 'C', 'E', 'Folate', 'B1'], minerals: ['Iron'], aminos: ['Asparagine'] } },
                    { name: 'Beets', color: 'text-b-vitamins', nutrition: { calories: 43, protein: 1.6, carbs: 10, fat: 0.2 }, nutrients: { vitamins: ['Folate'], minerals: ['Manganese', 'Potassium'], other: ['Nitrates'] } },
                    { name: 'Bell Pepper (Red)', color: 'text-vitamin-c', nutrition: { calories: 31, protein: 1, carbs: 6, fat: 0.3 }, nutrients: { vitamins: ['C', 'A', 'B6'], other: ['Capsanthin', 'Quercetin'] } },
                    { name: 'Bok Choy', color: 'text-vitamin-a', nutrition: { calories: 13, protein: 1.5, carbs: 2.2, fat: 0.2 }, nutrients: { vitamins: ['A', 'C', 'K'] } },
                    { name: 'Broccoli', color: 'text-vitamin-c', nutrition: { calories: 34, protein: 2.8, carbs: 7, fat: 0.4 }, nutrients: { vitamins: ['C', 'K1', 'A', 'Folate'], minerals: ['Potassium'], other: ['Sulforaphane'] } },
                    { name: 'Brussels Sprouts', color: 'text-vitamin-c', nutrition: { calories: 43, protein: 3.4, carbs: 9, fat: 0.3 }, nutrients: { vitamins: ['C', 'K'], minerals: ['Manganese'], other: ['Kaempferol'] } },
                    { name: 'Cabbage', color: 'text-vitamin-c', nutrition: { calories: 25, protein: 1.3, carbs: 6, fat: 0.1 }, nutrients: { vitamins: ['C', 'K'], other: ['Glucosinolates'] } },
                    { name: 'Carrot', color: 'text-vitamin-a', nutrition: { calories: 41, protein: 0.9, carbs: 10, fat: 0.2 }, nutrients: { vitamins: ['A', 'K1', 'B6'], other: ['Beta-carotene', 'Lutein'] } },
                    { name: 'Cauliflower', color: 'text-vitamin-c', nutrition: { calories: 25, protein: 1.9, carbs: 5, fat: 0.3 }, nutrients: { vitamins: ['C', 'K'], other: ['Fiber', 'Choline'] } },
                    { name: 'Celery', color: 'text-vitamin-k', nutrition: { calories: 16, protein: 0.7, carbs: 3, fat: 0.2 }, nutrients: { vitamins: ['K', 'A'], other: ['Apigenin'] } },
                    { name: 'Collard Greens', color: 'text-vitamin-k', nutrition: { calories: 32, protein: 3, carbs: 5, fat: 0.6 }, nutrients: { vitamins: ['K', 'A', 'C'], minerals: ['Calcium'] } },
                    { name: 'Corn', color: 'text-b-vitamins', nutrition: { calories: 86, protein: 3.2, carbs: 19, fat: 1.2 }, nutrients: { vitamins: ['B1', 'B9'], minerals: ['Phosphorus'], other: ['Lutein'] } },
                    { name: 'Cucumber', color: 'text-vitamin-k', nutrition: { calories: 15, protein: 0.7, carbs: 3.6, fat: 0.1 }, nutrients: { vitamins: ['K'], other: ['High water content'] } },
                    { name: 'Eggplant', color: 'text-vitamin-k', nutrition: { calories: 25, protein: 1, carbs: 6, fat: 0.2 }, nutrients: { vitamins: ['K', 'B1'], minerals: ['Manganese'], other: ['Nasunin'] } },
                    { name: 'Fennel', color: 'text-vitamin-c', nutrition: { calories: 31, protein: 1.2, carbs: 7, fat: 0.2 }, nutrients: { vitamins: ['C'], minerals: ['Potassium'], other: ['Anethole'] } },
                    { name: 'Garlic', color: 'text-vitamin-c', nutrition: { calories: 149, protein: 6.4, carbs: 33, fat: 0.5 }, nutrients: { vitamins: ['C', 'B6'], minerals: ['Manganese'], other: ['Allicin'] } },
                    { name: 'Ginger', color: 'text-enzymes', nutrition: { calories: 80, protein: 1.8, carbs: 18, fat: 0.8 }, nutrients: { minerals: ['Potassium'], enzymes: ['Zingibain'], other: ['Gingerol'] } },
                    { name: 'Green Beans', color: 'text-vitamin-k', nutrition: { calories: 31, protein: 1.8, carbs: 7, fat: 0.1 }, nutrients: { vitamins: ['K', 'C', 'A'] } },
                    { name: 'Jicama', color: 'text-vitamin-c', nutrition: { calories: 38, protein: 0.7, carbs: 9, fat: 0.1 }, nutrients: { vitamins: ['C'], other: ['Inulin Fiber'] } },
                    { name: 'Kale', color: 'text-vitamin-k', nutrition: { calories: 49, protein: 4.3, carbs: 9, fat: 0.9 }, nutrients: { vitamins: ['K', 'A', 'C'], minerals: ['Manganese'], other: ['Antioxidants'] } },
                    { name: 'Leeks', color: 'text-vitamin-k', nutrition: { calories: 61, protein: 1.5, carbs: 14, fat: 0.3 }, nutrients: { vitamins: ['K', 'A'], other: ['Kaempferol'] } },
                    { name: 'Lettuce (Romaine)', color: 'text-vitamin-a', nutrition: { calories: 17, protein: 1.2, carbs: 3.3, fat: 0.3 }, nutrients: { vitamins: ['A', 'K', 'Folate'] } },
                    { name: 'Mushrooms', color: 'text-b-vitamins', nutrition: { calories: 22, protein: 3.1, carbs: 3.3, fat: 0.3 }, nutrients: { vitamins: ['B2', 'B3', 'B5', 'D'], minerals: ['Selenium', 'Copper'], aminos: ['Glutamic Acid'] } },
                    { name: 'Okra', color: 'text-vitamin-k', nutrition: { calories: 33, protein: 1.9, carbs: 7, fat: 0.2 }, nutrients: { vitamins: ['K', 'C'], other: ['Mucilage'] } },
                    { name: 'Onion', color: 'text-vitamin-c', nutrition: { calories: 40, protein: 1.1, carbs: 9, fat: 0.1 }, nutrients: { vitamins: ['C', 'B6', 'Folate'], other: ['Quercetin'] } },
                    { name: 'Parsnip', color: 'text-vitamin-c', nutrition: { calories: 75, protein: 1.2, carbs: 18, fat: 0.3 }, nutrients: { vitamins: ['C', 'K', 'Folate'], minerals: ['Manganese'] } },
                    { name: 'Peas', color: 'text-vitamin-c', nutrition: { calories: 81, protein: 5.4, carbs: 14, fat: 0.4 }, nutrients: { vitamins: ['C', 'K', 'A', 'B1'], aminos: ['Lysine'] } },
                    { name: 'Potato', color: 'text-vitamin-c', nutrition: { calories: 77, protein: 2, carbs: 17, fat: 0.1 }, nutrients: { vitamins: ['C', 'B6'], minerals: ['Potassium'], other: ['Resistant Starch'] } },
                    { name: 'Pumpkin', color: 'text-vitamin-a', nutrition: { calories: 26, protein: 1, carbs: 7, fat: 0.1 }, nutrients: { vitamins: ['A', 'C', 'E'], other: ['Beta-carotene'] } },
                    { name: 'Radish', color: 'text-vitamin-c', nutrition: { calories: 16, protein: 0.7, carbs: 3.4, fat: 0.1 }, nutrients: { vitamins: ['C'], other: ['Isothiocyanates'] } },
                    { name: 'Seaweed (Nori)', color: 'text-b-vitamins', nutrition: { calories: 35, protein: 5.8, carbs: 5.1, fat: 0.3 }, nutrients: { vitamins: ['A', 'C', 'B12'], minerals: ['Iodine', 'Iron'] } },
                    { name: 'Spinach', color: 'text-vitamin-a', nutrition: { calories: 23, protein: 2.9, carbs: 3.6, fat: 0.4 }, nutrients: { vitamins: ['A', 'K', 'C', 'Folate'], minerals: ['Iron', 'Magnesium', 'Manganese'], other: ['Lutein'] } },
                    { name: 'Squash (Butternut)', color: 'text-vitamin-a', nutrition: { calories: 45, protein: 1, carbs: 12, fat: 0.1 }, nutrients: { vitamins: ['A', 'C', 'E', 'B6'], minerals: ['Magnesium'] } },
                    { name: 'Sweet Potato', color: 'text-vitamin-a', nutrition: { calories: 86, protein: 1.6, carbs: 20, fat: 0.1 }, nutrients: { vitamins: ['A', 'C', 'B6'], minerals: ['Manganese'], other: ['Beta-carotene'] } },
                    { name: 'Swiss Chard', color: 'text-vitamin-k', nutrition: { calories: 19, protein: 1.8, carbs: 3.7, fat: 0.2 }, nutrients: { vitamins: ['K', 'A', 'C'], minerals: ['Magnesium'] } },
                    { name: 'Tomato', color: 'text-vitamin-c', nutrition: { calories: 18, protein: 0.9, carbs: 3.9, fat: 0.2 }, nutrients: { vitamins: ['C', 'K', 'A'], minerals: ['Potassium'], other: ['Lycopene'] } },
                    { name: 'Turnip', color: 'text-vitamin-c', nutrition: { calories: 28, protein: 0.9, carbs: 6, fat: 0.1 }, nutrients: { vitamins: ['C'], minerals: ['Potassium'] } },
                    { name: 'Zucchini', color: 'text-vitamin-c', nutrition: { calories: 17, protein: 1.2, carbs: 3.1, fat: 0.3 }, nutrients: { vitamins: ['C', 'A', 'B6'] } },
                ],
                "Proteins": [
                    { name: 'Beef (lean)', color: 'text-iron', nutrition: { calories: 250, protein: 26, carbs: 0, fat: 15 }, nutrients: { vitamins: ['B12', 'B3', 'B6'], minerals: ['Iron', 'Zinc', 'Selenium'], aminos: ['All Essential'], other: ['Creatine', 'Taurine'] } },
                    { name: 'Bison', color: 'text-iron', nutrition: { calories: 143, protein: 28, carbs: 0, fat: 2.4 }, nutrients: { vitamins: ['B12'], minerals: ['Iron', 'Zinc', 'Selenium'], aminos: ['All Essential'] } },
                    { name: 'Chicken Breast', color: 'text-b-vitamins', nutrition: { calories: 165, protein: 31, carbs: 0, fat: 3.6 }, nutrients: { vitamins: ['B3', 'B6', 'B5'], minerals: ['Selenium', 'Phosphorus'], aminos: ['All Essential'] } },
                    { name: 'Cod', color: 'text-vitamin-d', nutrition: { calories: 82, protein: 18, carbs: 0, fat: 0.7 }, nutrients: { vitamins: ['D', 'B12', 'B6'], minerals: ['Iodine', 'Selenium'] } },
                    { name: 'Crab', color: 'text-zinc', nutrition: { calories: 83, protein: 18, carbs: 0, fat: 1.1 }, nutrients: { vitamins: ['B12'], minerals: ['Zinc', 'Copper', 'Selenium'] } },
                    { name: 'Duck', color: 'text-iron', nutrition: { calories: 337, protein: 19, carbs: 0, fat: 28 }, nutrients: { vitamins: ['B3'], minerals: ['Iron', 'Selenium'], aminos: ['All Essential'] } },
                    { name: 'Eggs', color: 'text-vitamin-d', nutrition: { calories: 155, protein: 13, carbs: 1.1, fat: 11 }, nutrients: { vitamins: ['D', 'B12', 'B2', 'A'], minerals: ['Selenium'], aminos: ['All Essential'], other: ['Choline'] } },
                    { name: 'Lamb', color: 'text-iron', nutrition: { calories: 294, protein: 25, carbs: 0, fat: 21 }, nutrients: { vitamins: ['B12', 'B3'], minerals: ['Iron', 'Zinc'], aminos: ['All Essential'] } },
                    { name: 'Lobster', color: 'text-zinc', nutrition: { calories: 77, protein: 16, carbs: 0.5, fat: 0.7 }, nutrients: { vitamins: ['B12'], minerals: ['Zinc', 'Copper', 'Selenium'] } },
                    { name: 'Mackerel', color: 'text-vitamin-d', nutrition: { calories: 205, protein: 18, carbs: 0, fat: 14 }, nutrients: { vitamins: ['D', 'B12'], other: ['Omega-3'] } },
                    { name: 'Oysters', color: 'text-zinc', nutrition: { calories: 199, protein: 9, carbs: 12, fat: 13 }, nutrients: { vitamins: ['D', 'B12'], minerals: ['Zinc', 'Iron', 'Copper'] } },
                    { name: 'Pork (lean)', color: 'text-b-vitamins', nutrition: { calories: 143, protein: 26, carbs: 0, fat: 3.5 }, nutrients: { vitamins: ['B1', 'B3', 'B6', 'B12'], minerals: ['Selenium'], aminos: ['All Essential'] } },
                    { name: 'Salmon', color: 'text-vitamin-d', nutrition: { calories: 208, protein: 20, carbs: 0, fat: 13 }, nutrients: { vitamins: ['D', 'B12', 'B3', 'B6'], minerals: ['Selenium'], other: ['Omega-3 Fatty Acids'] } },
                    { name: 'Sardines', color: 'text-calcium', nutrition: { calories: 208, protein: 25, carbs: 0, fat: 11 }, nutrients: { vitamins: ['D', 'B12'], minerals: ['Calcium', 'Selenium'], other: ['Omega-3'] } },
                    { name: 'Scallops', color: 'text-b-vitamins', nutrition: { calories: 88, protein: 17, carbs: 2.4, fat: 0.8 }, nutrients: { vitamins: ['B12'], minerals: ['Phosphorus', 'Selenium'] } },
                    { name: 'Shrimp', color: 'text-vitamin-d', nutrition: { calories: 85, protein: 20, carbs: 0.2, fat: 0.5 }, nutrients: { vitamins: ['D', 'B12'], minerals: ['Selenium', 'Iron'], other: ['Astaxanthin'] } },
                    { name: 'Trout', color: 'text-vitamin-d', nutrition: { calories: 148, protein: 21, carbs: 0, fat: 6.6 }, nutrients: { vitamins: ['D', 'B12'], other: ['Omega-3'] } },
                    { name: 'Tuna', color: 'text-vitamin-d', nutrition: { calories: 132, protein: 28, carbs: 0, fat: 1.3 }, nutrients: { vitamins: ['B12', 'D', 'B3'], minerals: ['Selenium'], other: ['Omega-3 Fatty Acids'] } },
                    { name: 'Turkey', color: 'text-b-vitamins', nutrition: { calories: 135, protein: 30, carbs: 0, fat: 1 }, nutrients: { vitamins: ['B3', 'B6'], minerals: ['Selenium', 'Zinc'], aminos: ['Tryptophan'] } },
                ],
                "Legumes, Nuts & Seeds": [
                    { name: 'Almonds', color: 'text-vitamin-e', nutrition: { calories: 579, protein: 21, carbs: 22, fat: 49 }, nutrients: { vitamins: ['E', 'B2'], minerals: ['Magnesium', 'Manganese'], other: ['Fiber', 'Antioxidants'] } },
                    { name: 'Black Beans', color: 'text-iron', nutrition: { calories: 132, protein: 8.9, carbs: 24, fat: 0.5 }, nutrients: { vitamins: ['Folate', 'B1'], minerals: ['Magnesium', 'Iron'], other: ['Fiber'] } },
                    { name: 'Brazil Nuts', color: 'text-vitamin-e', nutrition: { calories: 659, protein: 14, carbs: 12, fat: 67 }, nutrients: { vitamins: ['E'], minerals: ['Selenium', 'Magnesium'], aminos: ['Methionine'] } },
                    { name: 'Cashews', color: 'text-magnesium', nutrition: { calories: 553, protein: 18, carbs: 30, fat: 44 }, nutrients: { minerals: ['Magnesium', 'Copper', 'Manganese', 'Zinc'], aminos: ['Tryptophan'] } },
                    { name: 'Chia Seeds', color: 'text-calcium', nutrition: { calories: 486, protein: 17, carbs: 42, fat: 31 }, nutrients: { minerals: ['Calcium', 'Manganese', 'Magnesium'], other: ['Fiber', 'Omega-3 Fatty Acids'] } },
                    { name: 'Chickpeas', color: 'text-iron', nutrition: { calories: 164, protein: 8.9, carbs: 27, fat: 2.6 }, nutrients: { vitamins: ['Folate'], minerals: ['Manganese', 'Iron'], other: ['Fiber'] } },
                    { name: 'Edamame', color: 'text-vitamin-k', nutrition: { calories: 122, protein: 11, carbs: 10, fat: 5 }, nutrients: { vitamins: ['K', 'Folate'], minerals: ['Manganese'], aminos: ['All Essential'] } },
                    { name: 'Flax Seeds', color: 'text-b-vitamins', nutrition: { calories: 534, protein: 18, carbs: 29, fat: 42 }, nutrients: { vitamins: ['B1'], minerals: ['Magnesium'], other: ['Lignans', 'Omega-3'] } },
                    { name: 'Hazelnuts', color: 'text-vitamin-e', nutrition: { calories: 628, protein: 15, carbs: 17, fat: 61 }, nutrients: { vitamins: ['E'], minerals: ['Manganese', 'Copper'] } },
                    { name: 'Hemp Seeds', color: 'text-magnesium', nutrition: { calories: 553, protein: 31, carbs: 9, fat: 49 }, nutrients: { minerals: ['Magnesium', 'Iron', 'Zinc'], aminos: ['All Essential'] } },
                    { name: 'Kidney Beans', color: 'text-iron', nutrition: { calories: 127, protein: 8.7, carbs: 23, fat: 0.5 }, nutrients: { vitamins: ['Folate', 'B1'], minerals: ['Iron'] } },
                    { name: 'Lentils', color: 'text-iron', nutrition: { calories: 116, protein: 9, carbs: 20, fat: 0.4 }, nutrients: { vitamins: ['Folate', 'B1'], minerals: ['Iron', 'Manganese'], other: ['Fiber', 'Polyphenols'] } },
                    { name: 'Peanuts', color: 'text-vitamin-e', nutrition: { calories: 567, protein: 26, carbs: 16, fat: 49 }, nutrients: { vitamins: ['B3', 'E', 'B1'], minerals: ['Manganese', 'Magnesium'], other: ['Resveratrol'] } },
                    { name: 'Pecans', color: 'text-zinc', nutrition: { calories: 691, protein: 9, carbs: 14, fat: 72 }, nutrients: { minerals: ['Zinc', 'Manganese', 'Copper'] } },
                    { name: 'Pine Nuts', color: 'text-vitamin-e', nutrition: { calories: 673, protein: 14, carbs: 13, fat: 68 }, nutrients: { vitamins: ['E', 'K'], minerals: ['Manganese', 'Magnesium'] } },
                    { name: 'Pistachios', color: 'text-b-vitamins', nutrition: { calories: 562, protein: 20, carbs: 28, fat: 45 }, nutrients: { vitamins: ['B6', 'B1'], minerals: ['Copper', 'Manganese'] } },
                    { name: 'Pumpkin Seeds', color: 'text-magnesium', nutrition: { calories: 559, protein: 30, carbs: 11, fat: 49 }, nutrients: { minerals: ['Magnesium', 'Zinc', 'Manganese'], aminos: ['Tryptophan'], other: ['Antioxidants'] } },
                    { name: 'Sesame Seeds', color: 'text-calcium', nutrition: { calories: 573, protein: 18, carbs: 23, fat: 50 }, nutrients: { minerals: ['Calcium', 'Iron', 'Copper', 'Manganese'] } },
                    { name: 'Sunflower Seeds', color: 'text-vitamin-e', nutrition: { calories: 584, protein: 21, carbs: 20, fat: 51 }, nutrients: { vitamins: ['E', 'B1', 'B6'], minerals: ['Selenium', 'Magnesium'] } },
                    { name: 'Tofu', color: 'text-calcium', nutrition: { calories: 76, protein: 8, carbs: 1.9, fat: 4.8 }, nutrients: { minerals: ['Manganese', 'Calcium', 'Selenium'], aminos: ['All Essential'], other: ['Isoflavones'] } },
                    { name: 'Walnuts', color: 'text-b-vitamins', nutrition: { calories: 654, protein: 15, carbs: 14, fat: 65 }, nutrients: { minerals: ['Manganese', 'Copper', 'Magnesium'], other: ['Omega-3 Fatty Acids', 'Polyphenols'] } },
                ],
                "Grains": [
                    { name: 'Amaranth', color: 'text-iron', nutrition: { calories: 102, protein: 3.8, carbs: 19, fat: 1.6 }, nutrients: { minerals: ['Manganese', 'Magnesium', 'Iron'], aminos: ['Lysine'] } },
                    { name: 'Barley', color: 'text-b-vitamins', nutrition: { calories: 123, protein: 2.3, carbs: 28, fat: 0.4 }, nutrients: { vitamins: ['B1', 'B3'], minerals: ['Selenium', 'Manganese'], other: ['Beta-glucan'] } },
                    { name: 'Brown Rice', color: 'text-b-vitamins', nutrition: { calories: 111, protein: 2.6, carbs: 23, fat: 0.9 }, nutrients: { vitamins: ['B1', 'B3', 'B6'], minerals: ['Manganese', 'Magnesium', 'Selenium'], other: ['Fiber'] } },
                    { name: 'Buckwheat', color: 'text-magnesium', nutrition: { calories: 92, protein: 3.4, carbs: 20, fat: 0.6 }, nutrients: { minerals: ['Manganese', 'Magnesium', 'Copper'], other: ['Rutin'] } },
                    { name: 'Bulgur Wheat', color: 'text-iron', nutrition: { calories: 83, protein: 3.1, carbs: 19, fat: 0.2 }, nutrients: { minerals: ['Manganese', 'Magnesium', 'Iron'] } },
                    { name: 'Cornmeal', color: 'text-b-vitamins', nutrition: { calories: 367, protein: 9.4, carbs: 74, fat: 3.9 }, nutrients: { vitamins: ['B1', 'B9'], minerals: ['Iron'] } },
                    { name: 'Millet', color: 'text-magnesium', nutrition: { calories: 119, protein: 3.5, carbs: 24, fat: 0.7 }, nutrients: { minerals: ['Manganese', 'Magnesium', 'Phosphorus'] } },
                    { name: 'Oats', color: 'text-iron', nutrition: { calories: 389, protein: 17, carbs: 66, fat: 7 }, nutrients: { minerals: ['Manganese', 'Phosphorus', 'Magnesium'], other: ['Fiber (Beta-glucan)', 'Avenanthramides'] } },
                    { name: 'Quinoa', color: 'text-magnesium', nutrition: { calories: 120, protein: 4.4, carbs: 21, fat: 1.9 }, nutrients: { vitamins: ['Folate', 'B1', 'B2', 'B6'], minerals: ['Manganese', 'Magnesium', 'Iron'], aminos: ['All Essential'], other: ['Quercetin', 'Kaempferol'] } },
                    { name: 'Rye', color: 'text-iron', nutrition: { calories: 338, protein: 10, carbs: 76, fat: 1.6 }, nutrients: { minerals: ['Manganese', 'Copper', 'Magnesium'] } },
                    { name: 'Sorghum', color: 'text-iron', nutrition: { calories: 329, protein: 11, carbs: 72, fat: 3.5 }, nutrients: { minerals: ['Magnesium', 'Iron', 'Phosphorus'] } },
                    { name: 'Spelt', color: 'text-iron', nutrition: { calories: 127, protein: 5.5, carbs: 26, fat: 0.9 }, nutrients: { minerals: ['Manganese', 'Phosphorus', 'Magnesium'] } },
                    { name: 'Teff', color: 'text-iron', nutrition: { calories: 101, protein: 3.9, carbs: 20, fat: 0.7 }, nutrients: { minerals: ['Manganese', 'Iron', 'Magnesium', 'Calcium'] } },
                    { name: 'Wild Rice', color: 'text-zinc', nutrition: { calories: 101, protein: 4, carbs: 21, fat: 0.3 }, nutrients: { minerals: ['Zinc', 'Manganese', 'Phosphorus'] } },
                ],
                "Dairy & Alternatives": [
                    { name: 'Almond Milk', color: 'text-calcium', nutrition: { calories: 39, protein: 1, carbs: 3, fat: 2.5 }, nutrients: { vitamins: ['E', 'D (fortified)'], minerals: ['Calcium (fortified)'] } },
                    { name: 'Cheddar Cheese', color: 'text-calcium', nutrition: { calories: 404, protein: 23, carbs: 3.1, fat: 33 }, nutrients: { vitamins: ['A', 'B12', 'B2'], minerals: ['Calcium', 'Phosphorus', 'Zinc'] } },
                    { name: 'Cottage Cheese', color: 'text-calcium', nutrition: { calories: 81, protein: 12, carbs: 4.8, fat: 2.3 }, nutrients: { vitamins: ['B12', 'B2'], minerals: ['Calcium', 'Selenium'], aminos: ['Casein'] } },
                    { name: 'Feta Cheese', color: 'text-calcium', nutrition: { calories: 264, protein: 14, carbs: 4, fat: 21 }, nutrients: { vitamins: ['B12', 'B2'], minerals: ['Calcium', 'Sodium'] } },
                    { name: 'Goat Cheese', color: 'text-calcium', nutrition: { calories: 364, protein: 22, carbs: 0.1, fat: 30 }, nutrients: { vitamins: ['A', 'B2'], minerals: ['Copper', 'Calcium'] } },
                    { name: 'Greek Yogurt', color: 'text-calcium', nutrition: { calories: 59, protein: 10, carbs: 3.6, fat: 0.4 }, nutrients: { vitamins: ['B12', 'B2'], minerals: ['Calcium', 'Phosphorus'], other: ['Probiotics'] } },
                    { name: 'Kefir', color: 'text-calcium', nutrition: { calories: 104, protein: 9, carbs: 9, fat: 2.5 }, nutrients: { vitamins: ['D', 'B12'], minerals: ['Calcium'], other: ['Probiotics'] } },
                    { name: 'Milk', color: 'text-calcium', nutrition: { calories: 42, protein: 3.4, carbs: 5, fat: 1 }, nutrients: { vitamins: ['D', 'B12', 'B2'], minerals: ['Calcium', 'Phosphorus'] } },
                    { name: 'Mozzarella', color: 'text-calcium', nutrition: { calories: 280, protein: 28, carbs: 3.1, fat: 17 }, nutrients: { minerals: ['Calcium', 'Phosphorus'] } },
                    { name: 'Parmesan Cheese', color: 'text-calcium', nutrition: { calories: 431, protein: 38, carbs: 4.1, fat: 29 }, nutrients: { minerals: ['Calcium', 'Phosphorus'] } },
                    { name: 'Ricotta Cheese', color: 'text-calcium', nutrition: { calories: 174, protein: 11, carbs: 3, fat: 13 }, nutrients: { vitamins: ['A', 'B12'], minerals: ['Calcium', 'Selenium'] } },
                    { name: 'Soy Milk', color: 'text-calcium', nutrition: { calories: 45, protein: 3.3, carbs: 4.1, fat: 1.8 }, nutrients: { vitamins: ['D (fortified)', 'B12 (fortified)'], minerals: ['Calcium (fortified)'], aminos: ['All Essential'] } },
                ]
            };
            
            const mealIdeasData = {
                "Vegan Dishes": [
                    { name: "Lentil Shepherd's Pie", ingredients: "Lentils, mixed vegetables, sweet potato topping", steps: "1. Cook lentils with herbs. 2. Sauté vegetables. 3. Combine lentils and veggies in a dish. 4. Top with mashed sweet potato and bake." },
                    { name: "Black Bean Burgers on Gluten-Free Buns", ingredients: "Black beans, quinoa, spices, gluten-free buns", steps: "1. Mash black beans with cooked quinoa and spices. 2. Form patties and pan-fry or bake. 3. Serve on gluten-free buns with your favorite toppings." },
                    { name: "Quinoa Salad with Roasted Vegetables", ingredients: "Quinoa, bell peppers, zucchini, chickpeas, lemon vinaigrette", steps: "1. Cook quinoa. 2. Roast chopped vegetables and chickpeas. 3. Toss all ingredients with lemon vinaigrette." },
                    { name: "Creamy Tomato Soup with Cashew Cream", ingredients: "Tomatoes, onion, garlic, cashews", steps: "1. Sauté onion and garlic, add tomatoes and simmer. 2. Blend soup until smooth. 3. Blend soaked cashews with water to make cream and swirl into soup." },
                    { name: "Chickpea and Spinach Curry", ingredients: "Chickpeas, spinach, coconut milk, curry spices", steps: "1. Sauté onions and spices. 2. Add coconut milk, chickpeas, and simmer. 3. Stir in spinach until wilted. Serve with brown rice." },
                    { name: "Stuffed Bell Peppers with Wild Rice", ingredients: "Bell peppers, wild rice, mushrooms, black beans", steps: "1. Cook wild rice. 2. Sauté mushrooms and mix with rice and beans. 3. Stuff peppers and bake until tender." },
                    { name: "Vegan Pad Thai with Tofu", ingredients: "Rice noodles, tofu, bean sprouts, peanuts, Pad Thai sauce", steps: "1. Cook noodles. 2. Sauté tofu. 3. Combine all ingredients in a wok with sauce." },
                    { name: "Mushroom and Walnut Bolognese", ingredients: "Mushrooms, walnuts, tomatoes, herbs, gluten-free pasta", steps: "1. Finely chop mushrooms and walnuts. 2. Sauté and simmer in tomato sauce. 3. Serve over gluten-free pasta." },
                    { name: "Butternut Squash Risotto", ingredients: "Arborio rice, butternut squash, vegetable broth, nutritional yeast", steps: "1. Roast and mash squash. 2. Cook risotto, gradually adding broth. 3. Stir in squash and nutritional yeast." },
                    { name: "Spicy Peanut Noodles with Edamame", ingredients: "Gluten-free spaghetti, edamame, peanut sauce, red pepper flakes", steps: "1. Cook pasta. 2. Whisk together peanut sauce. 3. Toss pasta with sauce and steamed edamame." },
                    { name: "Sweet Potato and Kale Tacos", ingredients: "Corn tortillas, sweet potato, kale, avocado", steps: "1. Roast sweet potato cubes. 2. Sauté kale. 3. Serve in warm corn tortillas with mashed avocado." },
                    { name: "Cauliflower 'Steaks' with Chimichurri", ingredients: "Cauliflower, parsley, garlic, olive oil", steps: "1. Cut thick cauliflower slices and roast until tender. 2. Blend chimichurri ingredients. 3. Top steaks with sauce." },
                    { name: "Vegan Chili Sin Carne", ingredients: "Kidney beans, black beans, tomatoes, chili powder", steps: "1. Sauté onions and garlic. 2. Add beans, tomatoes, and spices. 3. Simmer for at least 30 minutes." },
                    { name: "Zucchini Noodles with Pesto", ingredients: "Zucchini, basil, pine nuts, nutritional yeast", steps: "1. Spiralize zucchini. 2. Blend pesto ingredients. 3. Toss zucchini noodles with fresh pesto." },
                    { name: "Tofu Scramble", ingredients: "Firm tofu, turmeric, black salt, vegetables", steps: "1. Crumble tofu into a pan. 2. Add turmeric for color and black salt for eggy flavor. 3. Sauté with your favorite veggies." },
                    { name: "Roasted Root Vegetable Medley", ingredients: "Carrots, parsnips, beets, rosemary", steps: "1. Chop vegetables. 2. Toss with olive oil and rosemary. 3. Roast until caramelized." },
                    { name: "Hearty Mushroom Stew", ingredients: "Mixed mushrooms, vegetable broth, potatoes, carrots", steps: "1. Sauté mushrooms. 2. Add vegetables and broth. 3. Simmer until vegetables are tender." },
                    { name: "Eggplant and Lentil Moussaka", ingredients: "Eggplant, lentils, tomato sauce, potato topping", steps: "1. Roast eggplant slices. 2. Make a lentil-tomato filling. 3. Layer and top with sliced potatoes, then bake." },
                    { name: "Jackfruit 'Pulled Pork' Sandwiches", ingredients: "Canned jackfruit, BBQ sauce, gluten-free buns", steps: "1. Shred jackfruit and simmer in BBQ sauce. 2. Serve on gluten-free buns with coleslaw." },
                    { name: "Vegan Sushi Rolls", ingredients: "Nori, sushi rice, avocado, cucumber, carrot", steps: "1. Prepare sushi rice. 2. Layer rice and fillings on nori. 3. Roll tightly and slice." },
                    { name: "Beetroot and Quinoa Salad", ingredients: "Cooked beets, quinoa, walnuts, balsamic glaze", steps: "1. Dice cooked beets. 2. Toss with quinoa and walnuts. 3. Drizzle with balsamic glaze." },
                    { name: "African Peanut Stew", ingredients: "Sweet potatoes, peanut butter, collard greens, tomatoes", steps: "1. Sauté onions. 2. Add sweet potatoes, tomatoes, and broth, simmer. 3. Stir in peanut butter and collard greens." },
                    { name: "Curried Red Lentil Soup", ingredients: "Red lentils, coconut milk, curry paste", steps: "1. Sauté onions and curry paste. 2. Add lentils and broth, simmer until soft. 3. Stir in coconut milk and blend if desired." },
                    { name: "Falafel Wraps with Tahini Sauce", ingredients: "Chickpeas, herbs, spices, gluten-free wraps, tahini", steps: "1. Blend chickpeas with herbs and spices. 2. Form balls and bake or air-fry. 3. Serve in wraps with tahini sauce." },
                    { name: "Miso Glazed Aubergine", ingredients: "Eggplant, miso paste, mirin, sesame seeds", steps: "1. Halve eggplant and score the flesh. 2. Brush with miso glaze. 3. Bake until soft and caramelized." },
                    { name: "Vegan Potato Salad", ingredients: "Potatoes, vegan mayo, celery, dill", steps: "1. Boil and dice potatoes. 2. Mix with vegan mayo, chopped celery, and fresh dill." },
                    { name: "One-Pot Gluten-Free Pasta", ingredients: "Gluten-free pasta, cherry tomatoes, basil, garlic", steps: "1. Combine all ingredients in a pot with water. 2. Bring to a boil and cook until pasta is done." },
                    { name: "Savory Steel Cut Oats", ingredients: "Gluten-free steel-cut oats, mushrooms, spinach, tamari", steps: "1. Cook oats in vegetable broth. 2. Sauté mushrooms and spinach. 3. Stir veggies into cooked oats with a splash of tamari." },
                    { name: "Cabbage Rolls Stuffed with Rice", ingredients: "Cabbage leaves, brown rice, mushrooms, tomato sauce", steps: "1. Steam cabbage leaves until pliable. 2. Make rice and mushroom filling. 3. Roll, cover with tomato sauce, and bake." },
                    { name: "Shepherdess Pie with Cauliflower Mash", ingredients: "Lentils, veggies, cauliflower", steps: "1. Make lentil and vegetable base. 2. Steam and mash cauliflower. 3. Top base with mash and bake." },
                    { name: "Spaghetti Squash with Marinara", ingredients: "Spaghetti squash, marinara sauce, herbs", steps: "1. Roast spaghetti squash. 2. Scrape out strands with a fork. 3. Top with your favorite marinara sauce." },
                    { name: "Black Rice Salad with Mango", ingredients: "Black rice, mango, red onion, cilantro-lime dressing", steps: "1. Cook black rice. 2. Dice mango and red onion. 3. Toss with dressing." },
                    { name: "Socca (Chickpea Flour Flatbread)", ingredients: "Chickpea flour, water, olive oil, herbs", steps: "1. Whisk ingredients together. 2. Pour into a hot, oiled skillet. 3. Cook like a pancake, flipping once." },
                    { name: "Creamy Polenta with Roasted Tomatoes", ingredients: "Polenta, cherry tomatoes, garlic, herbs", steps: "1. Cook polenta until creamy. 2. Roast cherry tomatoes with garlic. 3. Serve polenta topped with tomatoes." }
                ],
                "Smoothie Mixes": [
                    { name: "Green Detox", ingredients: "Spinach, banana, pineapple, coconut water", steps: "Blend all ingredients until smooth." },
                    { name: "Berry Antioxidant", ingredients: "Mixed berries, almond milk, chia seeds", steps: "Blend all ingredients until smooth." },
                    { name: "Tropical Sunshine", ingredients: "Mango, banana, orange juice, turmeric", steps: "Blend all ingredients until smooth." },
                    { name: "Peanut Butter Power", ingredients: "Banana, peanut butter, almond milk, protein powder", steps: "Blend all ingredients until smooth." },
                    { name: "Chocolate Avocado Dream", ingredients: "Avocado, cocoa powder, banana, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Kale and Apple Cleanser", ingredients: "Kale, green apple, cucumber, lemon juice", steps: "Blend all ingredients until smooth." },
                    { name: "Strawberry Banana Classic", ingredients: "Strawberries, banana, Greek yogurt (or vegan alternative)", steps: "Blend all ingredients until smooth." },
                    { name: "Pineapple Ginger Zinger", ingredients: "Pineapple, fresh ginger, banana, water", steps: "Blend all ingredients until smooth." },
                    { name: "Blueberry Muffin", ingredients: "Blueberries, gluten-free rolled oats, almond milk, cinnamon", steps: "Blend all ingredients until smooth." },
                    { name: "Coffee Lover's Boost", ingredients: "Chilled coffee, banana, protein powder, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Peach Cobbler", ingredients: "Peaches, gluten-free rolled oats, cinnamon, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Cherry Almond", ingredients: "Cherries, almond butter, almond milk, spinach", steps: "Blend all ingredients until smooth." },
                    { name: "Raspberry Lime Refresher", ingredients: "Raspberries, lime juice, banana, coconut water", steps: "Blend all ingredients until smooth." },
                    { name: "Matcha Energy", ingredients: "Matcha powder, banana, spinach, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Pumpkin Spice", ingredients: "Pumpkin puree, banana, pumpkin spice, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Watermelon Hydrator", ingredients: "Watermelon, mint, lime juice", steps: "Blend all ingredients until smooth." },
                    { name: "Acai Superfood", ingredients: "Acai packet, banana, berries, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Carrot Cake", ingredients: "Carrot, banana, walnuts, cinnamon, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Cinnamon Roll", ingredients: "Banana, gluten-free rolled oats, cinnamon, vanilla protein powder, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Key Lime Pie", ingredients: "Avocado, lime juice, banana, spinach, coconut milk", steps: "Blend all ingredients until smooth." },
                    { name: "Orange Creamsicle", ingredients: "Orange, banana, vanilla yogurt (or vegan alt)", steps: "Blend all ingredients until smooth." },
                    { name: "Beet and Berry", ingredients: "Cooked beet, mixed berries, ginger, water", steps: "Blend all ingredients until smooth." },
                    { name: "Fig and Almond", ingredients: "Dried figs, almond butter, banana, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Papaya Digestive Aid", ingredients: "Papaya, pineapple, ginger, coconut water", steps: "Blend all ingredients until smooth." },
                    { name: "Black Forest", ingredients: "Cherries, cocoa powder, spinach, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Grapefruit Glow", ingredients: "Grapefruit, pineapple, spinach, water", steps: "Blend all ingredients until smooth." },
                    { name: "Pina Colada", ingredients: "Pineapple, banana, coconut milk", steps: "Blend all ingredients until smooth." },
                    { name: "Apple Pie", ingredients: "Apple, gluten-free rolled oats, cinnamon, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Mocha Madness", ingredients: "Coffee, cocoa powder, banana, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Vanilla Bean", ingredients: "Banana, vanilla extract, protein powder, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Sweet Green", ingredients: "Kale, mango, banana, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Raspberry Avocado", ingredients: "Raspberries, avocado, spinach, water", steps: "Blend all ingredients until smooth." },
                    { name: "Blackberry Sage", ingredients: "Blackberries, fresh sage, banana, almond milk", steps: "Blend all ingredients until smooth." },
                    { name: "Cranberry Orange", ingredients: "Cranberries, orange, banana, water", steps: "Blend all ingredients until smooth." }
                ],
                "Healthy Dishes": [
                    { name: "Lemon Herb Baked Salmon", ingredients: "Salmon fillet, lemon, dill, parsley", steps: "1. Season salmon with herbs, salt, and pepper. 2. Top with lemon slices. 3. Bake at 400°F (200°C) for 12-15 minutes." },
                    { name: "Grilled Chicken with Roasted Asparagus", ingredients: "Chicken breast, asparagus, olive oil, herbs", steps: "1. Season chicken and grill until cooked through. 2. Toss asparagus with olive oil and roast until tender." },
                    { name: "Sheet Pan Chicken Fajitas", ingredients: "Chicken breast, bell peppers, onions, fajita seasoning", steps: "1. Slice chicken and veggies. 2. Toss with seasoning and oil on a sheet pan. 3. Bake at 400°F (200°C) for 20-25 minutes." },
                    { name: "Turkey Meatballs with Zucchini Noodles", ingredients: "Ground turkey, herbs, zucchini, marinara sauce", steps: "1. Form turkey meatballs and bake or pan-fry. 2. Spiralize zucchini. 3. Serve meatballs and marinara over zucchini noodles." },
                    { name: "Shrimp Scampi with Spaghetti Squash", ingredients: "Shrimp, garlic, lemon, spaghetti squash", steps: "1. Roast spaghetti squash and scrape strands. 2. Sauté shrimp with garlic and lemon juice. 3. Toss with squash strands." },
                    { name: "Blackened Tilapia with Mango Salsa", ingredients: "Tilapia fillets, blackening spice, mango, red onion, cilantro", steps: "1. Coat tilapia with spice and pan-sear. 2. Dice mango, onion, and cilantro for salsa. 3. Top fish with salsa." },
                    { name: "Chicken and Vegetable Skewers", ingredients: "Chicken chunks, cherry tomatoes, zucchini, bell peppers", steps: "1. Marinate chicken chunks. 2. Thread chicken and veggies onto skewers. 3. Grill or bake until cooked." },
                    { name: "Egg Roll in a Bowl", ingredients: "Ground chicken or turkey, coleslaw mix, coconut aminos, ginger", steps: "1. Brown ground meat. 2. Add coleslaw mix and seasonings. 3. Sauté until cabbage is tender." },
                    { name: "Stuffed Acorn Squash", ingredients: "Acorn squash, ground turkey, quinoa, cranberries", steps: "1. Roast acorn squash halves. 2. Cook ground turkey and quinoa. 3. Mix with cranberries, stuff squash, and bake again briefly." },
                    { name: "Seared Scallops with Cauliflower Puree", ingredients: "Sea scallops, cauliflower, garlic", steps: "1. Steam and blend cauliflower with garlic for puree. 2. Pat scallops dry and sear in a hot pan for 1-2 minutes per side." },
                    { name: "Chicken Lettuce Wraps", ingredients: "Ground chicken, water chestnuts, mushrooms, lettuce cups", steps: "1. Sauté ground chicken with finely chopped veggies. 2. Season with tamari or coconut aminos. 3. Serve in large lettuce leaves." },
                    { name: "Baked Cod with Tomatoes and Olives", ingredients: "Cod fillets, cherry tomatoes, olives, capers", steps: "1. Place cod in a baking dish. 2. Top with tomatoes, olives, and capers. 3. Bake until fish is flaky." },
                    { name: "Turkey and Bell Pepper Stir-fry", ingredients: "Ground turkey, bell peppers, broccoli, snap peas, gluten-free stir-fry sauce", steps: "1. Brown turkey. 2. Add veggies and stir-fry until tender-crisp. 3. Add sauce and serve." },
                    { name: "Salmon Cakes with Dill Sauce", ingredients: "Canned salmon, almond flour, egg, fresh dill, yogurt", steps: "1. Mix salmon, almond flour, and egg to form patties. 2. Pan-fry until golden. 3. Serve with a yogurt-dill sauce." },
                    { name: "Chicken Piccata with Capers", ingredients: "Chicken breast, lemon juice, capers, chicken broth", steps: "1. Sauté thinly sliced chicken breast. 2. Make a pan sauce with broth, lemon juice, and capers. 3. Pour sauce over chicken." },
                    { name: "Mediterranean Tuna Salad", ingredients: "Canned tuna, cucumber, tomatoes, olives, lemon vinaigrette", steps: "1. Flake tuna. 2. Mix with chopped veggies. 3. Dress with lemon vinaigrette. Serve in lettuce cups." },
                    { name: "Ground Chicken Stuffed Zucchini Boats", ingredients: "Zucchini, ground chicken, marinara, cheese (optional)", steps: "1. Hollow out zucchini halves. 2. Brown chicken and mix with marinara. 3. Fill zucchini and bake." },
                    { name: "Poached Fish in Coconut Curry Broth", ingredients: "White fish fillets, coconut milk, curry paste, spinach", steps: "1. Simmer coconut milk with curry paste. 2. Gently poach fish in the broth. 3. Wilt in spinach at the end." },
                    { name: "Chicken and Broccoli Casserole (Dairy-Free)", ingredients: "Cooked chicken, broccoli, cauliflower-cashew cream sauce", steps: "1. Combine chicken and broccoli in a dish. 2. Cover with a blended cauliflower-cashew cream sauce. 3. Bake until bubbly." },
                    { name: "Fish Tacos on Corn Tortillas", ingredients: "White fish, cabbage slaw, corn tortillas, avocado crema", steps: "1. Bake or grill seasoned fish. 2. Flake and serve in warm corn tortillas with slaw and avocado crema." },
                    { name: "Lemon Chicken and Rice Soup", ingredients: "Chicken breast, brown rice, carrots, celery, lemon", steps: "1. Simmer chicken and veggies in broth. 2. Shred chicken and add back to pot with cooked rice. 3. Finish with a squeeze of fresh lemon." },
                    { name: "Sausage and Peppers (Chicken/Turkey)", ingredients: "Chicken or turkey sausage, bell peppers, onions", steps: "1. Sauté sliced sausage. 2. Add sliced peppers and onions and cook until tender." },
                    { name: "Deconstructed Stuffed Pepper Skillet", ingredients: "Ground turkey, bell peppers, onions, cauliflower rice, tomatoes", steps: "1. Brown turkey with onions. 2. Add chopped peppers and tomatoes. 3. Stir in cauliflower rice and simmer." },
                    { name: "Thai Green Curry with Chicken", ingredients: "Chicken breast, green curry paste, coconut milk, bamboo shoots", steps: "1. Sauté chicken. 2. Add curry paste and coconut milk. 3. Simmer with bamboo shoots and other veggies." },
                    { name: "Herbed Turkey Burgers (No Bun)", ingredients: "Ground turkey, fresh herbs (parsley, thyme), served over greens", steps: "1. Mix herbs into ground turkey. 2. Form patties and grill or pan-fry. 3. Serve over a large salad." },
                    { name: "One-Pan Lemon Rosemary Chicken", ingredients: "Chicken thighs, potatoes, rosemary, lemon", steps: "1. Arrange chicken and potatoes on a sheet pan. 2. Season with rosemary, lemon, salt, and pepper. 3. Bake until cooked through." },
                    { name: "Garlic Shrimp with Quinoa", ingredients: "Shrimp, quinoa, garlic, parsley", steps: "1. Cook quinoa. 2. Sauté shrimp with garlic. 3. Toss with cooked quinoa and fresh parsley." },
                    { name: "Chicken Salad with Grapes and Walnuts", ingredients: "Cooked chicken, grapes, walnuts, yogurt-based dressing", steps: "1. Shred cooked chicken. 2. Mix with halved grapes and chopped walnuts. 3. Bind with a light yogurt dressing." },
                    { name: "Tuna Stuffed Avocados", ingredients: "Avocado, canned tuna, red onion, celery", steps: "1. Halve avocados and remove pits. 2. Mix tuna with finely chopped onion and celery. 3. Fill avocado halves with tuna salad." },
                    { name: "Baked Halibut with Green Beans", ingredients: "Halibut fillets, green beans, lemon, almonds", steps: "1. Place fish and green beans on a sheet pan. 2. Drizzle with olive oil and lemon juice. 3. Bake and top with toasted almonds." },
                    { name: "Ground Turkey and Sweet Potato Skillet", ingredients: "Ground turkey, sweet potato, black beans, spices", steps: "1. Brown turkey. 2. Add diced sweet potato and cook until tender. 3. Stir in black beans and spices." },
                    { name: "Coconut Lime Chicken", ingredients: "Chicken breast, coconut milk, lime juice, cilantro", steps: "1. Sauté chicken pieces. 2. Simmer in a sauce of coconut milk and lime juice. 3. Garnish with fresh cilantro." },
                    { name: "Mahi-Mahi with Pineapple Salsa", ingredients: "Mahi-mahi fillets, pineapple, red onion, jalapeño", steps: "1. Grill or pan-sear the fish. 2. Create a salsa with finely diced pineapple, onion, and jalapeño. 3. Top fish with salsa." },
                    { name: "Chicken and White Bean Soup", ingredients: "Chicken breast, cannellini beans, kale, vegetable broth", steps: "1. Sauté mirepoix (carrots, celery, onion). 2. Add broth, chicken, and beans. 3. Simmer, then shred chicken and add kale." },
                    { name: "Simple Poached Salmon", ingredients: "Salmon fillet, water or broth, lemon, herbs", steps: "1. Bring liquid to a gentle simmer. 2. Gently place salmon in the liquid. 3. Poach for 6-8 minutes until cooked." },
                    { name: "Turkey Chili", ingredients: "Ground turkey, kidney beans, tomatoes, chili powder", steps: "1. Brown turkey. 2. Add beans, tomatoes, and spices. 3. Simmer for at least 30 minutes." },
                    { name: "Greek Chicken Bowls", ingredients: "Chicken, quinoa, cucumber, tomatoes, olives, tzatziki", steps: "1. Grill seasoned chicken. 2. Assemble bowls with quinoa, chopped veggies, and chicken. 3. Top with tzatziki." },
                    { name: "Seared Ahi Tuna with Cauliflower Rice", ingredients: "Ahi tuna steak, cauliflower rice, sesame seeds, coconut aminos", steps: "1. Sear tuna briefly on each side. 2. Stir-fry cauliflower rice. 3. Serve sliced tuna over rice." },
                    { name: "Chicken Meatball and Veggie Soup", ingredients: "Ground chicken, carrots, celery, spinach, broth", steps: "1. Form small chicken meatballs. 2. Simmer meatballs and veggies in broth until cooked." },
                    { name: "Shrimp and Asparagus Stir-fry", ingredients: "Shrimp, asparagus, ginger, garlic, tamari", steps: "1. Stir-fry asparagus. 2. Add shrimp and cook through. 3. Add sauce and serve." },
                    { name: "Baked Chicken Thighs with Root Veggies", ingredients: "Chicken thighs, carrots, parsnips, sweet potatoes", steps: "1. Place chicken and chopped root veggies on a sheet pan. 2. Season and bake until chicken is cooked and veggies are tender." },
                    { name: "Frittata with Spinach and Mushrooms", ingredients: "Eggs, spinach, mushrooms, onion", steps: "1. Sauté veggies. 2. Pour whisked eggs over the top. 3. Bake until set." },
                    { name: "Salsa Verde Chicken", ingredients: "Chicken breast, salsa verde, onion, cilantro", steps: "1. Place chicken in a slow cooker. 2. Top with salsa verde and sliced onion. 3. Cook on low for 4-6 hours, then shred." },
                    { name: "Black Bean and Corn Salsa Chicken", ingredients: "Chicken breast, black beans, corn, salsa", steps: "1. Top chicken with salsa, beans, and corn in a baking dish. 2. Bake until chicken is cooked through." },
                    { name: "Honey Garlic Glazed Salmon", ingredients: "Salmon fillets, honey, garlic, coconut aminos", steps: "1. Whisk glaze ingredients. 2. Pour over salmon and bake, basting occasionally." },
                    { name: "Shepherd's Pie with Cauliflower Topping", ingredients: "Ground turkey, mixed veggies, cauliflower", steps: "1. Cook ground turkey and veggies in a savory sauce. 2. Top with steamed, mashed cauliflower. 3. Bake until golden." },
                    { name: "Unstuffed Cabbage Bowl", ingredients: "Ground turkey, cabbage, tomatoes, rice (or cauliflower rice)", steps: "1. Brown turkey. 2. Add chopped cabbage and tomatoes. 3. Simmer until cabbage is tender. Serve with rice." },
                    { name: "Pesto Chicken and Veggies", ingredients: "Chicken breast, cherry tomatoes, zucchini, pesto", steps: "1. Toss chicken and veggies with pesto. 2. Roast on a sheet pan until cooked." },
                    { name: "Spicy Shrimp with Broccoli", ingredients: "Shrimp, broccoli florets, red pepper flakes, garlic", steps: "1. Steam or roast broccoli. 2. Sauté shrimp with garlic and red pepper flakes. 3. Toss together." },
                    { name: "Curry Chicken Salad", ingredients: "Cooked chicken, yogurt, curry powder, celery, raisins", steps: "1. Shred chicken. 2. Mix with yogurt, curry powder, and other ingredients. Serve in lettuce cups." },
                    { name: "Italian Wedding Soup (No Pasta)", ingredients: "Turkey meatballs, spinach, carrots, celery, broth", steps: "1. Make small turkey meatballs. 2. Simmer in broth with veggies until cooked." },
                    { name: "Buffalo Chicken Stuffed Sweet Potatoes", ingredients: "Sweet potatoes, cooked shredded chicken, buffalo sauce", steps: "1. Bake sweet potatoes. 2. Toss chicken in buffalo sauce. 3. Stuff potatoes with chicken." },
                    { name: "Lemon Dill Tilapia", ingredients: "Tilapia fillets, lemon, fresh dill, olive oil", steps: "1. Season tilapia with dill, salt, and pepper. 2. Drizzle with olive oil and top with lemon slices. 3. Bake until flaky." },
                    { name: "Chicken and Asparagus Lemon Stir Fry", ingredients: "Chicken, asparagus, lemon, ginger", steps: "1. Stir-fry chicken. 2. Add asparagus and cook until tender-crisp. 3. Add a sauce of lemon juice and ginger." },
                    { name: "Smoked Salmon and Cucumber Bites", ingredients: "Cucumber, smoked salmon, dill cream cheese (or dairy-free alt)", steps: "1. Slice cucumber into thick rounds. 2. Top with a dollop of cream cheese and a piece of smoked salmon." }
                ]
            };

            const fitnessData = {
                "Cardio": [
                    { name: "Walking (brisk)", description: "A low-impact exercise that improves cardiovascular health.", calsPerMin: 5.0 },
                    { name: "Running / Jogging", description: "A high-impact exercise excellent for endurance and calorie burning.", calsPerMin: 11.5 },
                    { name: "Cycling (moderate)", description: "Great for leg strength and cardiovascular fitness with low impact.", calsPerMin: 8.0 },
                    { name: "Swimming (freestyle)", description: "A full-body, no-impact workout that builds endurance and muscle.", calsPerMin: 10.0 },
                    { name: "Jump Rope", description: "An intense cardio exercise that improves coordination and burns many calories.", calsPerMin: 12.0 },
                    { name: "Rowing Machine", description: "A full-body workout that combines cardio with strength training.", calsPerMin: 11.0 },
                    { name: "Stair Climbing", description: "An excellent way to build leg strength and cardiovascular endurance.", calsPerMin: 9.0 },
                    { name: "Elliptical Trainer", description: "A low-impact alternative to running that works the whole body.", calsPerMin: 9.5 },
                    { name: "HIIT (High-Intensity Interval Training)", description: "Short bursts of intense exercise followed by brief recovery periods.", calsPerMin: 14.0 },
                    { name: "Dancing (energetic)", description: "A fun way to get a full-body cardio workout.", calsPerMin: 7.5 },
                ],
                "Bodybuilding & Strength Training": [
                    { name: "Barbell Bench Press", description: "The classic chest builder, also works shoulders and triceps.", calsPerMin: 6.0 },
                    { name: "Barbell Squat", description: "A fundamental compound exercise for building lower body strength and size.", calsPerMin: 8.5 },
                    { name: "Barbell Deadlift", description: "A full-body strength builder, targeting the posterior chain.", calsPerMin: 9.0 },
                    { name: "Overhead Press (Barbell/Dumbbell)", description: "Builds shoulder strength and size.", calsPerMin: 6.0 },
                    { name: "Bent-Over Row (Barbell/Dumbbell)", description: "Develops back thickness and strength.", calsPerMin: 6.5 },
                    { name: "Dumbbell Lunges", description: "A unilateral exercise for building leg strength and stability.", calsPerMin: 7.0 },
                    { name: "Bicep Curls (Dumbbell/Barbell)", description: "Isolation exercise for the biceps.", calsPerMin: 4.0 },
                    { name: "Tricep Dips", description: "Using parallel bars or a bench to build tricep strength.", calsPerMin: 5.5 },
                    { name: "Lat Pulldowns", description: "Machine exercise to develop back width.", calsPerMin: 5.0 },
                    { name: "Leg Press", description: "Machine exercise for building quadriceps and glutes.", calsPerMin: 7.0 },
                    { name: "Dumbbell Flyes", description: "Chest isolation exercise to stretch and build the pectoral muscles.", calsPerMin: 4.5 },
                    { name: "Lateral Raises", description: "Shoulder isolation exercise for the medial deltoid.", calsPerMin: 4.0 },
                    { name: "Calf Raises", description: "Isolation exercise for the calf muscles.", calsPerMin: 3.5 },
                    { name: "Leg Curls", description: "Machine exercise to isolate the hamstrings.", calsPerMin: 4.0 },
                    { name: "Leg Extensions", description: "Machine exercise to isolate the quadriceps.", calsPerMin: 4.0 },
                ],
                "Powerlifting & Olympic Lifting": [
                    { name: "Powerlifting Squat", description: "Low-bar squat focused on moving maximum weight.", calsPerMin: 9.0 },
                    { name: "Powerlifting Bench Press", description: "Arch-backed press focused on moving maximum weight.", calsPerMin: 6.5 },
                    { name: "Sumo Deadlift", description: "Wide-stance deadlift variation common in powerlifting.", calsPerMin: 9.5 },
                    { name: "Conventional Deadlift", description: "Narrow-stance deadlift focused on maximum weight.", calsPerMin: 9.5 },
                    { name: "Snatch", description: "Olympic lift moving a barbell from the floor to overhead in one motion.", calsPerMin: 13.0 },
                    { name: "Clean and Jerk", description: "Olympic lift moving a barbell from floor to shoulders, then to overhead.", calsPerMin: 12.5 },
                    { name: "Power Clean", description: "Explosive pull of a barbell from the floor to the shoulders.", calsPerMin: 11.0 },
                    { name: "Push Press", description: "Overhead press using leg drive to move more weight.", calsPerMin: 8.0 },
                    { name: "Front Squat", description: "Squat with the barbell held in a front rack position.", calsPerMin: 8.0 },
                ],
                "Calisthenics": [
                    { name: "Push-ups", description: "Classic bodyweight exercise for chest, shoulders, and triceps.", calsPerMin: 8.0 },
                    { name: "Pull-ups / Chin-ups", description: "Bodyweight exercise for back and bicep strength.", calsPerMin: 9.0 },
                    { name: "Bodyweight Squats", description: "Fundamental lower body exercise using only body weight.", calsPerMin: 7.0 },
                    { name: "Plank", description: "Isometric core exercise for stability.", calsPerMin: 3.0 },
                    { name: "Burpees", description: "A full-body, high-intensity exercise combining a squat, push-up, and jump.", calsPerMin: 15.0 },
                    { name: "Mountain Climbers", description: "A dynamic core exercise that also elevates the heart rate.", calsPerMin: 10.0 },
                    { name: "Jumping Jacks", description: "A classic full-body cardio and coordination exercise.", calsPerMin: 8.5 },
                    { name: "Handstand Push-ups", description: "Advanced exercise for shoulder strength and balance.", calsPerMin: 10.0 },
                    { name: "Muscle-ups", description: "Advanced movement combining a pull-up and a dip.", calsPerMin: 12.0 },
                    { name: "L-Sits", description: "Isometric core and hip flexor exercise.", calsPerMin: 5.0 },
                ],
                "Yoga, Pilates & Mind-Body": [
                    { name: "Yoga (Vinyasa Flow)", description: "A dynamic style of yoga connecting movement with breath.", calsPerMin: 5.5 },
                    { name: "Yoga (Hatha)", description: "A slower-paced yoga focusing on basic poses and breathing.", calsPerMin: 3.0 },
                    { name: "Pilates", description: "Focuses on core strength, flexibility, and body awareness.", calsPerMin: 4.5 },
                    { name: "Tai Chi", description: "A gentle, flowing martial art that promotes balance and relaxation.", calsPerMin: 4.0 },
                    { name: "Stretching", description: "Improves flexibility and range of motion.", calsPerMin: 2.5 },
                ],
                "Martial Arts": [
                    { name: "Taekwondo (forms/sparring)", description: "Korean martial art known for its dynamic kicking techniques.", calsPerMin: 10.0 },
                    { name: "Kung Fu (training)", description: "Chinese martial arts with a wide variety of styles and forms.", calsPerMin: 10.5 },
                    { name: "Boxing (bag work)", description: "High-intensity workout improving cardio and upper body strength.", calsPerMin: 12.0 },
                    { name: "Kickboxing", description: "Combines boxing punches with martial arts kicks for a full-body workout.", calsPerMin: 11.0 },
                    { name: "Judo / Jiu-Jitsu (drilling)", description: "Grappling arts that provide an intense full-body workout.", calsPerMin: 10.0 },
                ],
                "Functional & Unconventional": [
                    { name: "Kettlebell Swings", description: "A powerful, explosive exercise for the posterior chain and cardio.", calsPerMin: 13.0 },
                    { name: "Medicine Ball Slams", description: "A full-body power and cardio exercise.", calsPerMin: 10.0 },
                    { name: "Sandbag Lifts / Carries", description: "Builds functional, real-world strength and stability.", calsPerMin: 8.5 },
                    { name: "Farmer's Walk", description: "Builds grip strength, core stability, and work capacity.", calsPerMin: 7.5 },
                    { name: "Suitcase Carry", description: "A one-sided farmer's walk that heavily engages the obliques.", calsPerMin: 7.0 },
                    { name: "Tire Flips", description: "A full-body power exercise common in strongman training.", calsPerMin: 12.0 },
                    { name: "Sled Push / Pull", description: "Develops leg power and cardiovascular conditioning with no impact.", calsPerMin: 11.5 },
                    { name: "Battle Ropes", description: "An upper-body and core-focused cardio exercise.", calsPerMin: 12.5 },
                ],
                "Plyometrics": [
                    { name: "Box Jumps", description: "Explosive exercise for developing lower body power.", calsPerMin: 10.0 },
                    { name: "Broad Jumps", description: "Jumping for maximum distance to build horizontal power.", calsPerMin: 9.0 },
                    { name: "Plyo Push-ups", description: "An explosive push-up where the hands leave the ground.", calsPerMin: 9.5 },
                    { name: "Tuck Jumps", description: "Jumping and bringing the knees to the chest to build explosive power.", calsPerMin: 11.0 },
                    { name: "Depth Jumps", description: "Stepping off a box and immediately jumping for height.", calsPerMin: 9.0 },
                ],
            };
            const workoutRoutines = {
                "20-Minute Workouts": [
                    { name: "Quick HIIT Circuit", duration: "20 Minutes", focus: "Full Body Cardio", routine: "Perform each exercise for 40 seconds, followed by 20 seconds of rest. Complete 4 rounds: 1. Jumping Jacks 2. Bodyweight Squats 3. Push-ups 4. Mountain Climbers 5. Burpees" },
                    { name: "Core Blast", duration: "20 Minutes", focus: "Core Strength", routine: "Perform each exercise for 45 seconds, with 15 seconds rest. Complete 3 rounds: 1. Plank 2. Leg Raises 3. Bicycle Crunches 4. Russian Twists 5. Superman Holds" },
                    { name: "Kettlebell Burn", duration: "20 Minutes", focus: "Full Body Strength & Cardio", routine: "As Many Rounds As Possible (AMRAP) in 20 minutes: 10 Kettlebell Swings, 8 Goblet Squats, 6 Push-ups." },
                ],
                "30-45 Minute Workouts": [
                    { name: "Classic Push Day", duration: "45 Minutes", focus: "Chest, Shoulders, Triceps", routine: "1. Barbell Bench Press: 3 sets of 8-12 reps. 2. Overhead Press: 3 sets of 8-12 reps. 3. Incline Dumbbell Press: 3 sets of 10-15 reps. 4. Lateral Raises: 3 sets of 12-15 reps. 5. Tricep Dips: 3 sets to failure." },
                    { name: "Classic Pull Day", duration: "45 Minutes", focus: "Back, Biceps", routine: "1. Pull-ups (or Lat Pulldowns): 3 sets to failure (or 8-12 reps). 2. Bent-Over Rows: 3 sets of 8-12 reps. 3. Seated Cable Rows: 3 sets of 10-15 reps. 4. Face Pulls: 3 sets of 15-20 reps. 5. Bicep Curls: 3 sets of 10-15 reps." },
                    { name: "Classic Leg Day", duration: "45 Minutes", focus: "Lower Body", routine: "1. Barbell Squats: 3 sets of 8-12 reps. 2. Romanian Deadlifts: 3 sets of 10-15 reps. 3. Walking Lunges: 3 sets of 10-12 reps per leg. 4. Leg Press: 3 sets of 12-15 reps. 5. Calf Raises: 4 sets of 15-20 reps." },
                    { name: "Full Body Dumbbell", duration: "40 Minutes", focus: "Full Body Strength", routine: "Complete 3 rounds of this circuit: 1. Dumbbell Goblet Squats (12 reps) 2. Dumbbell Bench Press (12 reps) 3. Dumbbell Rows (12 reps per arm) 4. Dumbbell Overhead Press (12 reps) 5. Dumbbell Farmer's Walk (45 seconds). Rest 60-90 seconds between rounds." },
                    { name: "Vinyasa Yoga Flow", duration: "45 Minutes", focus: "Flexibility & Mind-Body", routine: "A continuous flow of poses including Sun Salutations, Warrior series, balancing poses like Tree Pose, and finishing with gentle stretches and Savasana (corpse pose)." },
                    { name: "Pilates Mat Routine", duration: "40 Minutes", focus: "Core & Stability", routine: "A series of classic Pilates exercises such as The Hundred, Roll Up, Leg Circles, and Criss-Cross, focusing on precise movements and core engagement." },
                ],
                "60-90 Minute Workouts": [
                    { name: "Powerlifting Session", duration: "90 Minutes", focus: "Max Strength", routine: "1. Main Lift (Squat, Bench, or Deadlift): Work up to a heavy set of 3-5 reps. 2. Accessory Lift 1: 3-4 sets of 6-10 reps (e.g., Overhead Press after Bench). 3. Accessory Lift 2: 3-4 sets of 8-12 reps (e.g., Rows after Bench). 4. Isolation/Core work: 3 sets of 10-15 reps." },
                    { name: "Bodybuilding Split (Chest & Triceps)", duration: "75 Minutes", focus: "Hypertrophy", routine: "1. Incline Barbell Press (4x8-12) 2. Flat Dumbbell Press (4x10-15) 3. Cable Crossovers (3x15-20) 4. Skull Crushers (4x10-15) 5. Tricep Pushdowns (4x12-15) 6. Overhead Tricep Extension (3x12-15)." },
                    { name: "Calisthenics Skill & Strength", duration: "90 Minutes", focus: "Bodyweight Mastery", routine: "1. Warm-up & Wrist Prep (10 mins). 2. Skill Work (e.g., Handstand practice) (20 mins). 3. Strength Circuit (5 rounds): 5 Muscle-ups (or 10 Pull-ups), 15 Dips, 20 Pistol Squats (10 per leg). 4. Core Work: 3 sets of L-Sits to failure. 5. Cool-down stretch." },
                    { name: "Long Run", duration: "60-90 Minutes", focus: "Cardio Endurance", routine: "Maintain a steady, conversational pace for the entire duration. Focus on consistent breathing and form." },
                    { name: "Functional Fitness Circuit", duration: "60 Minutes", focus: "Work Capacity & Strength", routine: "5 rounds for time: 400m Run, 20 Kettlebell Swings, 15 Wall Balls, 10 Burpees." }
                ],
            };
            
            // --- Navigation Logic ---
            function switchTab(tabName) {
                Object.values(menuItems).forEach(item => item.classList.remove('active'));
                healthHubMenu.classList.remove('active');
                
                Object.values(sections).forEach(section => section.classList.add('hidden'));

                const selectedMenuItem = menuItems[tabName];
                if (selectedMenuItem) {
                    sections[tabName].classList.remove('hidden');
                    if (selectedMenuItem.closest('.dropdown')) {
                        healthHubMenu.classList.add('active');
                    } else {
                        selectedMenuItem.classList.add('active');
                    }
                }
            }

            for (const key in menuItems) {
                menuItems[key].addEventListener('click', (e) => {
                    e.preventDefault();
                    switchTab(key);
                    healthHubDropdown.classList.remove('show');
                });
            }

            healthHubMenu.addEventListener('click', (e) => {
                e.stopPropagation();
                healthHubDropdown.classList.toggle('show');
            });

            document.addEventListener('click', (e) => {
                if (!healthHubMenu.contains(e.target)) {
                    healthHubDropdown.classList.remove('show');
                }
            });

            // --- Vitamin Calculator Logic ---
            nutritionGenderSelect.addEventListener('change', (e) => {
                nutritionGenderOtherContainer.classList.toggle('hidden', e.target.value !== 'other');
            });

            vitaminForm.addEventListener('submit', function(e) {
                e.preventDefault();
                const age = parseFloat(document.getElementById('nutrition-age').value);
                const gender = document.getElementById('nutrition-gender').value;
                const weight = parseFloat(document.getElementById('weight').value);
                let height = parseFloat(document.getElementById('height').value);
                const heightUnit = document.getElementById('height-unit').value;
                const activityLevel = parseFloat(document.getElementById('activity-level').value);

                if (isNaN(age) || isNaN(weight) || isNaN(height) || age <= 0 || weight <= 0 || height <= 0) {
                    const tempAlert = document.createElement('div');
                    tempAlert.className = 'bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative my-4';
                    tempAlert.textContent = 'Please enter valid age, weight, and height.';
                    vitaminForm.prepend(tempAlert);
                    setTimeout(() => tempAlert.remove(), 3000);
                    return;
                }
                
                // Convert height to cm if in inches
                if (heightUnit === 'in') {
                    height = height * 2.54;
                }

                let bmr;
                if (gender === 'male') {
                    bmr = 10 * weight + 6.25 * height - 5 * age + 5;
                } else if (gender === 'female') {
                    bmr = 10 * weight + 6.25 * height - 5 * age - 161;
                } else { // For 'prefer_not_to_say' and 'other', use an average
                    bmr = 10 * weight + 6.25 * height - 5 * age - 78;
                }

                const tdee = bmr * activityLevel;
                
                calculatedNeeds = {}; // Reset
                resultsGrid.innerHTML = ''; 
                Object.entries(vitaminData).forEach(([vitamin, data]) => {
                    let card;
                    if (data.unit === 'complex' || data.unit === 'essential' || data.unit === 'digestive') {
                        card = `<div class="card p-4 flex flex-col items-center text-center"><h4 class="text-lg font-bold ${data.color}">${vitamin}</h4><p class="text-gray-400 mt-2">Requirement varies. Focus on a balanced diet.</p></div>`;
                    } else {
                        const calculatedAmount = data.base + (tdee / 100) * data.multiplier;
                        calculatedNeeds[vitamin] = { amount: calculatedAmount.toFixed(1), unit: data.unit };
                        card = `<div class="card p-4 flex flex-col items-center text-center"><h4 class="text-lg font-bold ${data.color}">${vitamin}</h4><p class="text-3xl font-bold text-white mt-2">${calculatedAmount.toFixed(1)} <span class="text-lg font-normal">${data.unit}</span></p><p class="text-sm text-gray-500">per day</p></div>`;
                    }
                    resultsGrid.innerHTML += card;
                });

                resultsSection.classList.remove('hidden');
                geminiCtaContainer.classList.remove('hidden');
                geminiResultsSection.classList.add('hidden'); // Hide old results
                resultsSection.scrollIntoView({ behavior: 'smooth' });
            });
            
            // --- Activity Planner Logic ---
            activityGenderSelect.addEventListener('change', (e) => {
                activityGenderOtherContainer.classList.toggle('hidden', e.target.value !== 'other');
            });

            activityForm.addEventListener('submit', (e) => {
                e.preventDefault();
                const age = parseInt(document.getElementById('activity-age').value);
                if (isNaN(age) || age <= 0) {
                    const tempAlert = document.createElement('div');
                    tempAlert.className = 'bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative my-4';
                    tempAlert.textContent = 'Please enter a valid age.';
                    activityForm.prepend(tempAlert);
                    setTimeout(() => tempAlert.remove(), 3000);
                    return;
                }
                activityResultsSection.classList.remove('hidden');
                activityResultsSection.scrollIntoView({ behavior: 'smooth' });
            });
            
            // --- Gemini API Logic ---
            generateMealBtn.addEventListener('click', async () => {
                geminiResultsSection.classList.remove('hidden');
                geminiContent.innerHTML = '';
                geminiLoading.style.display = 'flex';
                geminiResultsSection.scrollIntoView({ behavior: 'smooth' });

                // Create a randomized, focused prompt for Gemini
                const needsKeys = Object.keys(calculatedNeeds);
                let randomNeeds = [];
                while(randomNeeds.length < 4 && needsKeys.length > 0) {
                    const randomIndex = Math.floor(Math.random() * needsKeys.length);
                    randomNeeds.push(needsKeys.splice(randomIndex, 1)[0]);
                }
                const neededNutrients = randomNeeds.join(', ');

                const prompt = `I need a simple, healthy, and gluten-free meal idea (like breakfast, lunch, or dinner) that is rich in the following nutrients: ${neededNutrients}. The meal should not contain pork or lamb. Please provide a creative recipe title, a short description, a list of ingredients, and simple, step-by-step instructions. Format the response cleanly using markdown-style headings (e.g., **Title**), bullet points for ingredients (* ingredient), and numbered steps for instructions (1. Step one).`;
                
                try {
                    const text = await callGemini(prompt);
                    let html = text
                        .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>')
                        .replace(/^\* (.*$)/gim, '<li class="ml-4 list-disc">$1</li>')
                        .replace(/^\d+\. (.*$)/gim, '<li class="ml-4 list-decimal">$1</li>')
                        .replace(/(\r\n|\n|\r)/gm, "<br>");
                    geminiContent.innerHTML = html;
                } catch (error) {
                    console.error("Gemini API call failed:", error);
                    geminiContent.innerHTML = `<p class="text-red-500">Sorry, we couldn't generate a meal idea at this time. Please try again later.</p>`;
                } finally {
                    geminiLoading.style.display = 'none';
                }
            });

            async function callGemini(prompt) {
                const apiKey = ""; // This will be handled by the execution environment
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;
                
                const payload = { contents: [{ role: "user", parts: [{ text: prompt }] }] };

                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) { throw new Error(`API request failed with status ${response.status}`); }
                const result = await response.json();

                if (result.candidates?.[0]?.content?.parts?.[0]?.text) {
                    return result.candidates[0].content.parts[0].text;
                } else {
                    console.error("Unexpected API response structure:", result);
                    throw new Error(result.error?.message || "No content received from API.");
                }
            }

            // --- Meal Ideas Population ---
            function populateMealIdeas() {
                mealIdeasGrid.innerHTML = '';
                for (const category in mealIdeasData) {
                    const categoryHeader = document.createElement('h2');
                    categoryHeader.className = 'text-2xl font-bold category-heading';
                    categoryHeader.textContent = category;
                    mealIdeasGrid.appendChild(categoryHeader);

                    const container = document.createElement('div');
                    container.className = 'grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6';

                    mealIdeasData[category].forEach(meal => {
                        const card = document.createElement('div');
                        card.className = 'card interactive-card p-6';
                        card.innerHTML = `
                            <div class="flex justify-between items-start">
                                <h4 class="text-xl font-bold text-indigo-400">${meal.name}</h4>
                                <svg class="w-4 h-4 text-gray-400 transform transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path></svg>
                            </div>
                            <p class="text-gray-400 mt-2 mb-4 text-sm"><strong>Key Ingredients:</strong> ${meal.ingredients}</p>
                            <div class="details-content prose prose-sm prose-invert max-w-none text-gray-300 pt-4 mt-4 border-t border-gray-700">
                                <p>${meal.steps}</p>
                            </div>
                        `;
                        card.addEventListener('click', () => {
                            card.classList.toggle('open');
                            card.querySelector('svg').classList.toggle('rotate-180');
                        });
                        container.appendChild(card);
                    });
                    mealIdeasGrid.appendChild(container);
                }
            }

            // --- Food List Population & Search ---
            function createNutrientPills(nutrients) {
                let pills = '';
                if (nutrients.vitamins?.length) pills += nutrients.vitamins.map(v => `<span class="inline-block bg-vitamin-c rounded-full px-2 py-1 text-xs font-semibold mr-1 mb-1">Vit ${v}</span>`).join('');
                if (nutrients.minerals?.length) pills += nutrients.minerals.map(m => `<span class="inline-block bg-minerals rounded-full px-2 py-1 text-xs font-semibold mr-1 mb-1">${m}</span>`).join('');
                if (nutrients.aminos?.length) pills += nutrients.aminos.map(a => `<span class="inline-block bg-amino-acids rounded-full px-2 py-1 text-xs font-semibold mr-1 mb-1">${a}</span>`).join('');
                if (nutrients.enzymes?.length) pills += nutrients.enzymes.map(e => `<span class="inline-block bg-enzymes rounded-full px-2 py-1 text-xs font-semibold mr-1 mb-1">${e}</span>`).join('');
                if (nutrients.other?.length) pills += nutrients.other.map(o => `<span class="inline-block bg-other rounded-full px-2 py-1 text-xs font-semibold mr-1 mb-1">${o}</span>`).join('');
                return pills;
            }

            function populateFoodList() {
                foodGrid.innerHTML = '';
                for (const category in foodData) {
                    const categoryHeader = document.createElement('h2');
                    categoryHeader.className = 'text-2xl font-bold category-heading';
                    categoryHeader.textContent = category;
                    categoryHeader.dataset.categoryHeader = category;
                    foodGrid.appendChild(categoryHeader);
                    
                    foodData[category].forEach(food => {
                        const nutrientPills = createNutrientPills(food.nutrients);

                        const nutritionFacts = food.nutrition ? `
                            <div class="details-content pt-4 mt-4 border-t border-gray-700">
                                <h5 class="font-bold text-gray-300 mb-2">Nutrition per 100g:</h5>
                                <ul class="text-sm text-gray-400 space-y-1">
                                    <li><strong>Calories:</strong> ${food.nutrition.calories} kcal</li>
                                    <li><strong>Protein:</strong> ${food.nutrition.protein} g</li>
                                    <li><strong>Carbs:</strong> ${food.nutrition.carbs} g</li>
                                    <li><strong>Fat:</strong> ${food.nutrition.fat} g</li>
                                </ul>
                            </div>
                        ` : '';

                        const card = document.createElement('div');
                        card.className = 'card interactive-card p-6';
                        card.dataset.foodCard = '';
                        card.dataset.foodName = food.name.toLowerCase();
                        card.dataset.foodCategory = category;
                        card.innerHTML = `
                            <div class="flex justify-between items-start">
                                <h4 class="text-xl font-bold ${food.color}">${food.name}</h4>
                                <svg class="w-4 h-4 text-gray-400 transform transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path></svg>
                            </div>
                            <p class="text-gray-400 mt-2 mb-4 text-sm">Contains:</p>
                            <div class="flex flex-wrap">${nutrientPills}</div>
                            ${nutritionFacts}
                        `;
                        foodGrid.appendChild(card);
                    });
                }
                
                document.querySelectorAll('[data-food-card]').forEach(card => {
                    card.addEventListener('click', () => {
                        card.classList.toggle('open');
                        card.querySelector('svg').classList.toggle('rotate-180');
                    });
                });
            }

            foodSearchInput.addEventListener('input', (e) => {
                const query = e.target.value.toLowerCase().trim();
                document.querySelectorAll('[data-food-card]').forEach(card => {
                    const isVisible = card.dataset.foodName.includes(query);
                    card.style.display = isVisible ? '' : 'none';
                });

                document.querySelectorAll('[data-category-header]').forEach(header => {
                    const category = header.dataset.categoryHeader;
                    const cardsInCategory = document.querySelectorAll(`[data-food-category="${category}"]`);
                    const anyVisible = Array.from(cardsInCategory).some(card => card.style.display !== 'none');
                    header.style.display = anyVisible ? '' : 'none';
                });
            });

            // --- Nutrient Info Population & Search ---
            function populateInfoList() {
                infoGrid.innerHTML = '';
                for (const category in nutrientInfoData) {
                    const categoryHeader = document.createElement('h2');
                    categoryHeader.className = 'text-3xl font-bold text-white mb-4';
                    categoryHeader.textContent = category;
                    categoryHeader.dataset.nutrientCategoryHeader = '';
                    infoGrid.appendChild(categoryHeader);

                    for (const subCategory in nutrientInfoData[category]) {
                        const subCategoryHeader = document.createElement('h3');
                        subCategoryHeader.className = 'text-2xl font-semibold text-gray-300 mt-6 mb-3 border-b border-gray-700 pb-2';
                        subCategoryHeader.textContent = subCategory;
                        subCategoryHeader.dataset.nutrientSubcategoryHeader = '';
                        infoGrid.appendChild(subCategoryHeader);

                        const container = document.createElement('div');
                        container.className = 'grid grid-cols-1 md:grid-cols-2 gap-4';
                        
                        nutrientInfoData[category][subCategory].forEach(item => {
                            const card = document.createElement('div');
                            card.className = 'card p-4';
                            card.dataset.nutrientCard = '';
                            card.dataset.nutrientName = item.name.toLowerCase();
                            card.innerHTML = `
                                <h4 class="font-bold text-lg text-indigo-400">${item.name}</h4>
                                <p class="text-gray-400 mt-2">${item.info}</p>
                            `;
                            container.appendChild(card);
                        });
                        infoGrid.appendChild(container);
                    }
                }
            }

            nutrientSearchInput.addEventListener('input', (e) => {
                const query = e.target.value.toLowerCase().trim();
                document.querySelectorAll('[data-nutrient-card]').forEach(card => {
                    const isVisible = card.dataset.nutrientName.includes(query);
                    card.style.display = isVisible ? '' : 'none';
                });

                document.querySelectorAll('[data-nutrient-subcategory-header]').forEach(header => {
                    const anyVisible = Array.from(header.nextElementSibling.children).some(card => card.style.display !== 'none');
                    header.style.display = anyVisible ? '' : 'none';
                });
                
                document.querySelectorAll('[data-nutrient-category-header]').forEach(header => {
                    const anySubVisible = Array.from(header.parentElement.querySelectorAll('[data-nutrient-subcategory-header]')).some(sub => sub.style.display !== 'none');
                    header.style.display = anySubVisible ? '' : 'none';
                });
            });

             // --- Fitness Hub Logic ---
            fitnessTabExercises.addEventListener('click', () => {
                fitnessTabExercises.classList.add('border-indigo-400', 'text-indigo-400');
                fitnessTabExercises.classList.remove('text-gray-500');
                fitnessTabRoutines.classList.remove('border-indigo-400', 'text-indigo-400');
                fitnessTabRoutines.classList.add('text-gray-500');
                fitnessExercisesContent.classList.remove('hidden');
                fitnessRoutinesContent.classList.add('hidden');
            });

            fitnessTabRoutines.addEventListener('click', () => {
                fitnessTabRoutines.classList.add('border-indigo-400', 'text-indigo-400');
                fitnessTabRoutines.classList.remove('text-gray-500');
                fitnessTabExercises.classList.remove('border-indigo-400', 'text-indigo-400');
                fitnessTabExercises.classList.add('text-gray-500');
                fitnessRoutinesContent.classList.remove('hidden');
                fitnessExercisesContent.classList.add('hidden');
            });
            
            function populateFitnessHub() {
                // Populate Exercises
                exerciseGrid.innerHTML = '';
                for (const category in fitnessData) {
                    const categoryHeader = document.createElement('h2');
                    categoryHeader.className = 'text-2xl font-bold category-heading';
                    categoryHeader.textContent = category;
                    exerciseGrid.appendChild(categoryHeader);

                    const container = document.createElement('div');
                    container.className = 'grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6';

                    fitnessData[category].forEach(ex => {
                        const card = document.createElement('div');
                        card.className = 'card p-4';
                        card.dataset.exerciseName = ex.name.toLowerCase();
                        card.innerHTML = `
                            <h4 class="font-bold text-lg text-indigo-400">${ex.name}</h4>
                            <p class="text-sm text-gray-400 mt-1">${ex.description}</p>
                            <p class="text-right font-bold text-pink-400 mt-2">~${ex.calsPerMin.toFixed(1)} cal/min</p>
                        `;
                        container.appendChild(card);
                    });
                    exerciseGrid.appendChild(container);
                }

                // Populate Routines
                routinesGrid.innerHTML = '';
                 for (const category in workoutRoutines) {
                    const categoryHeader = document.createElement('h2');
                    categoryHeader.className = 'text-2xl font-bold category-heading';
                    categoryHeader.textContent = category;
                    routinesGrid.appendChild(categoryHeader);
                    
                    const container = document.createElement('div');
                    container.className = 'grid grid-cols-1 md:grid-cols-2 gap-6';

                    workoutRoutines[category].forEach(routine => {
                        const card = document.createElement('div');
                        card.className = 'card interactive-card p-6';
                        card.innerHTML = `
                             <div class="flex justify-between items-start">
                                <h4 class="text-xl font-bold text-indigo-400">${routine.name}</h4>
                                <svg class="w-4 h-4 text-gray-400 transform transition-transform duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path></svg>
                            </div>
                            <p class="text-gray-400 mt-2 mb-4 text-sm"><strong>Duration:</strong> ${routine.duration} | <strong>Focus:</strong> ${routine.focus}</p>
                            <div class="details-content prose prose-sm prose-invert max-w-none text-gray-300 pt-4 mt-4 border-t border-gray-700">
                                <p>${routine.routine.replace(/\n/g, '<br>')}</p>
                            </div>
                        `;
                        card.addEventListener('click', () => {
                            card.classList.toggle('open');
                            card.querySelector('svg').classList.toggle('rotate-180');
                        });
                        container.appendChild(card);
                    });
                    routinesGrid.appendChild(container);
                }
            }

            exerciseSearchInput.addEventListener('input', (e) => {
                const query = e.target.value.toLowerCase().trim();
                document.querySelectorAll('[data-exercise-name]').forEach(card => {
                    const isVisible = card.dataset.exerciseName.includes(query);
                    card.style.display = isVisible ? '' : 'none';
                });

                // Hide category headers if all items within are hidden
                document.querySelectorAll('#exercise-grid .category-heading').forEach(header => {
                    const container = header.nextElementSibling;
                    const anyVisible = Array.from(container.children).some(card => card.style.display !== 'none');
                    header.style.display = anyVisible ? '' : 'none';
                });
            });

            // --- Zoom Logic ---
            zoomInBtn.addEventListener('click', () => {
                currentZoom = Math.min(1.5, currentZoom + 0.1);
                mainContent.style.transform = `scale(${currentZoom})`;
                mainContent.style.transformOrigin = 'top';
            });

            zoomOutBtn.addEventListener('click', () => {
                currentZoom = Math.max(0.7, currentZoom - 0.1);
                mainContent.style.transform = `scale(${currentZoom})`;
                mainContent.style.transformOrigin = 'top';
            });

            // --- Speech Synthesis Logic ---
            speakBtn.addEventListener('click', () => {
                if (synth.speaking) {
                    synth.cancel();
                    return;
                }
                
                let activeSection;
                for (const key in sections) {
                    if (!sections[key].classList.contains('hidden')) {
                        activeSection = sections[key];
                        break;
                    }
                }

                if (activeSection) {
                    const elementsToRead = activeSection.querySelectorAll('h2, h3, h4, p, label, span:not(.menu-item)');
                    const textToSpeak = Array.from(elementsToRead)
                        .map(el => el.textContent.trim())
                        .filter(text => text.length > 0)
                        .join('. ');

                    if (textToSpeak) {
                        utterance = new SpeechSynthesisUtterance(textToSpeak);
                        utterance.onstart = () => speakBtn.classList.add('bg-pink-500');
                        utterance.onend = () => speakBtn.classList.remove('bg-pink-500');
                        utterance.onerror = (event) => {
                            console.error('SpeechSynthesisUtterance.onerror', event);
                            speakBtn.classList.remove('bg-pink-500');
                        };
                        synth.speak(utterance);
                    }
                }
            });


            // --- Initializations ---
            populateFoodList();
            populateInfoList();
            populateMealIdeas();
            populateFitnessHub();
            switchTab('calculator');
        });
    </script>
</body>
</html>
