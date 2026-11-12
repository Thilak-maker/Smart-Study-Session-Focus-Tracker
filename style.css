<!DOCTYPE html>
<html lang="en" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Study Session & Focus Tracker</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js for Analytics -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Google Fonts: Inter & JetBrains Mono -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
    <!-- Font Awesome for clean icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        mono: ['JetBrains Mono', 'monospace'],
                    },
                    colors: {
                        slate: {
                            850: '#151e2e',
                            950: '#0a0f1a',
                        }
                    }
                }
            }
        }
    </script>
</head>
<body class="bg-slate-50 text-slate-800 dark:bg-slate-950 dark:text-slate-100 min-h-screen transition-colors duration-300 font-sans selection:bg-indigo-500 selection:text-white">

    <!-- Toast Notification Container (Replaces alert()) -->
    <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- Custom Confirmation Modal (Replaces confirm()) -->
    <div id="confirm-modal" class="fixed inset-0 bg-slate-950/70 backdrop-blur-sm z-50 hidden items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 rounded-2xl max-w-md w-full p-6 shadow-2xl transform transition-all">
            <div class="flex items-center gap-3 text-amber-500 mb-3">
                <i class="fa-solid fa-triangle-exclamation text-xl"></i>
                <h3 id="modal-title" class="text-lg font-semibold text-slate-900 dark:text-white">Confirm Action</h3>
            </div>
            <p id="modal-message" class="text-sm text-slate-600 dark:text-slate-400 mb-6">Are you sure you want to proceed?</p>
            <div class="flex justify-end gap-3">
                <button id="modal-cancel" class="px-4 py-2 rounded-xl text-sm font-medium bg-slate-100 hover:bg-slate-200 dark:bg-slate-800 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-300 transition">Cancel</button>
                <button id="modal-confirm" class="px-4 py-2 rounded-xl text-sm font-medium bg-rose-600 hover:bg-rose-700 text-white shadow-lg shadow-rose-500/20 transition">Confirm</button>
            </div>
        </div>
    </div>

    <!-- Top Navigation Bar -->
    <header class="sticky top-0 z-30 bg-white/80 dark:bg-slate-900/80 backdrop-blur-md border-b border-slate-200 dark:border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="w-9 h-9 rounded-xl bg-indigo-600 flex items-center justify-center text-white shadow-lg shadow-indigo-500/30">
                    <i class="fa-solid fa-brain text-lg"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg tracking-tight text-slate-900 dark:text-white leading-none">FocusFlow</h1>
                    <p class="text-xs text-slate-500 dark:text-slate-400 mt-0.5">Smart Study & Distraction Tracker</p>
                </div>
            </div>

            <div class="flex items-center gap-2 sm:gap-3">
                <!-- Demo Data Button -->
                <button onclick="loadDemoData()" class="px-3 py-2 rounded-xl text-xs sm:text-sm font-medium bg-indigo-50 hover:bg-indigo-100 dark:bg-indigo-500/10 dark:hover:bg-indigo-500/20 text-indigo-600 dark:text-indigo-400 border border-indigo-200 dark:border-indigo-500/20 transition flex items-center gap-1.5" title="Load sample study data">
                    <i class="fa-solid fa-wand-magic-sparkles"></i>
                    <span class="hidden sm:inline">Demo Data</span>
                </button>
                
                <!-- Clear Data Button -->
                <button onclick="promptClearData()" class="px-3 py-2 rounded-xl text-xs sm:text-sm font-medium bg-slate-100 hover:bg-rose-50 dark:bg-slate-800 dark:hover:bg-rose-950/50 text-slate-600 hover:text-rose-600 dark:text-slate-400 dark:hover:text-rose-400 border border-slate-200 dark:border-slate-700 transition flex items-center gap-1.5" title="Reset all progress">
                    <i class="fa-solid fa-trash-can"></i>
                    <span class="hidden sm:inline">Reset</span>
                </button>

                <!-- Theme Toggle -->
                <button id="theme-toggle" class="w-9 h-9 rounded-xl bg-slate-100 hover:bg-slate-200 dark:bg-slate-800 dark:hover:bg-slate-700 flex items-center justify-center text-slate-600 dark:text-slate-300 transition" aria-label="Toggle theme">
                    <i id="theme-icon" class="fa-solid fa-sun"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content Grid -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 sm:py-8">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 lg:gap-8">
            
            <!-- LEFT COLUMN: Pomodoro Timer & Distraction Logger (5 cols on lg) -->
            <div class="lg:col-span-5 flex flex-col gap-6">
                
                <!-- Pomodoro Card -->
                <section class="bg-white dark:bg-slate-900 rounded-3xl p-6 sm:p-8 border border-slate-200 dark:border-slate-800 shadow-xl shadow-slate-200/50 dark:shadow-none relative overflow-hidden">
                    <!-- Subtle background glow -->
                    <div id="timer-glow" class="absolute -top-24 -right-24 w-48 h-48 bg-indigo-500/10 rounded-full blur-3xl pointer-events-none transition-colors duration-500"></div>

                    <!-- Mode Switcher Pills -->
                    <div class="flex p-1 bg-slate-100 dark:bg-slate-850 rounded-2xl mb-6 border border-slate-200/60 dark:border-slate-800">
                        <button id="mode-study" onclick="switchMode('study')" class="flex-1 py-2.5 px-4 rounded-xl text-sm font-semibold transition-all bg-white dark:bg-indigo-600 text-indigo-600 dark:text-white shadow-sm">
                            <i class="fa-solid fa-book-open mr-1.5"></i> Study Focus
                        </button>
                        <button id="mode-break" onclick="switchMode('break')" class="flex-1 py-2.5 px-4 rounded-xl text-sm font-semibold transition-all text-slate-600 dark:text-slate-400 hover:text-slate-900 dark:hover:text-white">
                            <i class="fa-solid fa-mug-hot mr-1.5"></i> Short Break
                        </button>
                    </div>

                    <!-- Subject Tagging Selector -->
                    <div id="subject-section" class="mb-6 transition-opacity duration-300">
                        <label class="block text-xs font-semibold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-2">
                            Active Study Subject
                        </label>
                        <div class="flex gap-2">
                            <div class="relative flex-1">
                                <select id="subject-select" class="w-full appearance-none bg-slate-50 dark:bg-slate-850 border border-slate-200 dark:border-slate-700 rounded-xl px-4 py-2.5 text-sm font-medium text-slate-800 dark:text-slate-200 focus:outline-none focus:ring-2 focus:ring-indigo-500 transition">
                                    <!-- Populated via JS -->
                                </select>
                                <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-3 text-slate-400">
                                    <i class="fa-solid fa-chevron-down text-xs"></i>
                                </div>
                            </div>
                            <button onclick="toggleNewSubjectInput()" class="px-3.5 py-2.5 rounded-xl bg-slate-100 hover:bg-slate-200 dark:bg-slate-800 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-300 text-sm font-medium transition" title="Add custom subject">
                                <i class="fa-solid fa-plus"></i>
                            </button>
                        </div>

                        <!-- Hidden Add Subject Input -->
                        <div id="new-subject-box" class="hidden mt-2 flex gap-2">
                            <input type="text" id="new-subject-input" placeholder="e.g., Biology, Algorithms..." maxlength="24" class="flex-1 bg-slate-50 dark:bg-slate-850 border border-slate-200 dark:border-slate-700 rounded-xl px-3.5 py-2 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            <button onclick="addNewSubject()" class="px-4 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-sm font-medium transition">Add</button>
                        </div>
                    </div>

                    <!-- Circular SVG Progress Timer -->
                    <div class="relative w-56 h-56 sm:w-64 sm:h-64 mx-auto my-4 flex items-center justify-center">
                        <svg class="w-full h-full transform -rotate-90" viewBox="0 0 100 100">
                            <!-- Track Circle -->
                            <circle cx="50" cy="50" r="44" fill="transparent" stroke="currentColor" stroke-width="5" class="text-slate-100 dark:text-slate-800" />
                            <!-- Progress Circle -->
                            <circle id="timer-ring" cx="50" cy="50" r="44" fill="transparent" stroke="currentColor" stroke-width="5" stroke-linecap="round" stroke-dasharray="276.46" stroke-dashoffset="0" class="text-indigo-600 dark:text-indigo-500 transition-all duration-500" />
                        </svg>
                        <div class="absolute inset-0 flex flex-col items-center justify-center text-center">
                            <span id="timer-status-badge" class="text-xs font-semibold uppercase tracking-widest text-indigo-600 dark:text-indigo-400 mb-1">Ready</span>
                            <div id="timer-display" class="font-mono text-5xl sm:text-6xl font-bold tracking-tight text-slate-900 dark:text-white">
                                25:00
                            </div>
                            <span id="active-subject-label" class="text-xs text-slate-500 dark:text-slate-400 mt-2 max-w-[140px] truncate">Mathematics</span>
                        </div>
                    </div>

                    <!-- Timer Controls -->
                    <div class="flex items-center justify-center gap-3 mt-6">
                        <button id="btn-start-pause" onclick="toggleTimer()" class="flex-1 max-w-[180px] py-3.5 px-6 rounded-2xl bg-indigo-600 hover:bg-indigo-700 active:scale-[0.98] text-white font-semibold text-base shadow-lg shadow-indigo-600/25 transition flex items-center justify-center gap-2">
                            <i id="start-pause-icon" class="fa-solid fa-play"></i>
                            <span id="start-pause-text">Start</span>
                        </button>
                        <button onclick="resetTimer()" class="p-3.5 rounded-2xl bg-slate-100 hover:bg-slate-200 dark:bg-slate-800 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-300 transition" title="Reset Timer">
                            <i class="fa-solid fa-rotate-right text-lg"></i>
                        </button>
                        <button onclick="completeSessionEarly()" class="p-3.5 rounded-2xl bg-slate-100 hover:bg-emerald-50 dark:bg-slate-800 dark:hover:bg-emerald-950/50 text-slate-700 hover:text-emerald-600 dark:text-slate-300 dark:hover:text-emerald-400 transition" title="Finish & Log Session Now">
                            <i class="fa-solid fa-check text-lg"></i>
                        </button>
                    </div>

                    <!-- Custom Interval Settings -->
                    <div class="mt-6 pt-5 border-t border-slate-100 dark:border-slate-800/80 grid grid-cols-2 gap-4">
                        <div>
                            <label for="study-duration-input" class="block text-xs text-slate-500 dark:text-slate-400 mb-1">Study (mins)</label>
                            <input type="number" id="study-duration-input" value="25" min="1" max="180" onchange="updateCustomDurations()" class="w-full bg-slate-50 dark:bg-slate-850 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-1.5 text-sm font-mono font-medium focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        </div>
                        <div>
                            <label for="break-duration-input" class="block text-xs text-slate-500 dark:text-slate-400 mb-1">Break (mins)</label>
                            <input type="number" id="break-duration-input" value="5" min="1" max="60" onchange="updateCustomDurations()" class="w-full bg-slate-50 dark:bg-slate-850 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-1.5 text-sm font-mono font-medium focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        </div>
                    </div>
                </section>

                <!-- Distraction Quick-Logger Card -->
                <section class="bg-white dark:bg-slate-900 rounded-3xl p-6 border border-slate-200 dark:border-slate-800 shadow-lg shadow-slate-200/40 dark:shadow-none">
                    <div class="flex items-center justify-between mb-4">
                        <div>
                            <h2 class="text-base font-bold text-slate-900 dark:text-white flex items-center gap-2">
                                <i class="fa-solid fa-bolt text-amber-500"></i> Distraction Logger
                            </h2>
                            <p class="text-xs text-slate-500 dark:text-slate-400">Tap whenever your focus drifts to spot patterns</p>
                        </div>
                        <span id="session-distraction-badge" class="px-2.5 py-1 rounded-full text-xs font-semibold bg-amber-100 text-amber-800 dark:bg-amber-500/15 dark:text-amber-400">
                            0 logged today
                        </span>
                    </div>

                    <!-- Quick Log Buttons -->
                    <div class="grid grid-cols-2 gap-2.5 mb-4">
                        <button onclick="logDistraction('Phone / Notifications')" class="p-3 rounded-2xl bg-slate-50 hover:bg-amber-50 dark:bg-slate-850 dark:hover:bg-amber-500/10 border border-slate-200/80 dark:border-slate-800 hover:border-amber-300 dark:hover:border-amber-500/30 text-left transition group flex items-center gap-3">
                            <div class="w-8 h-8 rounded-xl bg-rose-100 dark:bg-rose-500/20 text-rose-600 dark:text-rose-400 flex items-center justify-center shrink-0 group-hover:scale-110 transition">
                                <i class="fa-solid fa-mobile-screen"></i>
                            </div>
                            <div class="overflow-hidden">
                                <div class="text-xs font-semibold text-slate-800 dark:text-slate-200 truncate">Phone</div>
                                <div class="text-[11px] text-slate-400 truncate">Texts & alerts</div>
                            </div>
                        </button>

                        <button onclick="logDistraction('Social Media / Web')" class="p-3 rounded-2xl bg-slate-50 hover:bg-amber-50 dark:bg-slate-850 dark:hover:bg-amber-500/10 border border-slate-200/80 dark:border-slate-800 hover:border-amber-300 dark:hover:border-amber-500/30 text-left transition group flex items-center gap-3">
                            <div class="w-8 h-8 rounded-xl bg-sky-100 dark:bg-sky-500/20 text-sky-600 dark:text-sky-400 flex items-center justify-center shrink-0 group-hover:scale-110 transition">
                                <i class="fa-solid fa-globe"></i>
                            </div>
                            <div class="overflow-hidden">
                                <div class="text-xs font-semibold text-slate-800 dark:text-slate-200 truncate">Social / Web</div>
                                <div class="text-[11px] text-slate-400 truncate">Mindless browsing</div>
                            </div>
                        </button>

                        <button onclick="logDistraction('Fatigue / Daydreaming')" class="p-3 rounded-2xl bg-slate-50 hover:bg-amber-50 dark:bg-slate-850 dark:hover:bg-amber-500/10 border border-slate-200/80 dark:border-slate-800 hover:border-amber-300 dark:hover:border-amber-500/30 text-left transition group flex items-center gap-3">
                            <div class="w-8 h-8 rounded-xl bg-purple-100 dark:bg-purple-500/20 text-purple-600 dark:text-purple-400 flex items-center justify-center shrink-0 group-hover:scale-110 transition">
                                <i class="fa-solid fa-battery-quarter"></i>
                            </div>
                            <div class="overflow-hidden">
                                <div class="text-xs font-semibold text-slate-800 dark:text-slate-200 truncate">Fatigue</div>
                                <div class="text-[11px] text-slate-400 truncate">Low energy / drift</div>
                            </div>
                        </button>

                        <button onclick="logDistraction('Environment / Noise')" class="p-3 rounded-2xl bg-slate-50 hover:bg-amber-50 dark:bg-slate-850 dark:hover:bg-amber-500/10 border border-slate-200/80 dark:border-slate-800 hover:border-amber-300 dark:hover:border-amber-500/30 text-left transition group flex items-center gap-3">
                            <div class="w-8 h-8 rounded-xl bg-amber-100 dark:bg-amber-500/20 text-amber-600 dark:text-amber-400 flex items-center justify-center shrink-0 group-hover:scale-110 transition">
                                <i class="fa-solid fa-volume-high"></i>
                            </div>
                            <div class="overflow-hidden">
                                <div class="text-xs font-semibold text-slate-800 dark:text-slate-200 truncate">Noise</div>
                                <div class="text-[11px] text-slate-400 truncate">People / surroundings</div>
                            </div>
                        </button>
                    </div>

                    <!-- Recent Distractions Mini-Feed -->
                    <div class="bg-slate-50 dark:bg-slate-850 rounded-2xl p-3 border border-slate-200/60 dark:border-slate-800/80">
                        <div class="text-[11px] font-semibold uppercase tracking-wider text-slate-400 mb-2 flex justify-between">
                            <span>Recent Logs</span>
                            <span id="current-session-distractions">Current session: 0</span>
                        </div>
                        <div id="distraction-feed" class="space-y-1.5 max-h-28 overflow-y-auto text-xs">
                            <p class="text-slate-400 italic py-2 text-center">No distractions logged yet. Stay sharp!</p>
                        </div>
                    </div>
                </section>

            </div>

            <!-- RIGHT COLUMN: Analytics Dashboard & History (7 cols on lg) -->
            <div class="lg:col-span-7 flex flex-col gap-6">
                
                <!-- KPI Summary Row -->
                <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 sm:gap-4">
                    <div class="bg-white dark:bg-slate-900 p-4 rounded-2xl border border-slate-200 dark:border-slate-800">
                        <div class="text-xs font-medium text-slate-500 dark:text-slate-400">Total Focus</div>
                        <div id="kpi-total-time" class="text-xl sm:text-2xl font-bold text-slate-900 dark:text-white mt-1">0m</div>
                        <div class="text-[11px] text-emerald-600 dark:text-emerald-400 mt-1 flex items-center gap-1">
                            <i class="fa-solid fa-clock"></i> Logged time
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-900 p-4 rounded-2xl border border-slate-200 dark:border-slate-800">
                        <div class="text-xs font-medium text-slate-500 dark:text-slate-400">Sessions</div>
                        <div id="kpi-total-sessions" class="text-xl sm:text-2xl font-bold text-slate-900 dark:text-white mt-1">0</div>
                        <div class="text-[11px] text-indigo-600 dark:text-indigo-400 mt-1 flex items-center gap-1">
                            <i class="fa-solid fa-fire"></i> Completed
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-900 p-4 rounded-2xl border border-slate-200 dark:border-slate-800">
                        <div class="text-xs font-medium text-slate-500 dark:text-slate-400">Top Subject</div>
                        <div id="kpi-top-subject" class="text-lg sm:text-xl font-bold text-slate-900 dark:text-white mt-1 truncate">—</div>
                        <div class="text-[11px] text-slate-500 dark:text-slate-400 mt-1 truncate" id="kpi-top-subject-sub">No data yet</div>
                    </div>

                    <div class="bg-white dark:bg-slate-900 p-4 rounded-2xl border border-slate-200 dark:border-slate-800">
                        <div class="text-xs font-medium text-slate-500 dark:text-slate-400">Distractions</div>
                        <div id="kpi-total-distractions" class="text-xl sm:text-2xl font-bold text-slate-900 dark:text-white mt-1">0</div>
                        <div class="text-[11px] text-amber-600 dark:text-amber-400 mt-1 truncate" id="kpi-top-distraction">Clear mind</div>
                    </div>
                </div>

                <!-- Charts Grid -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Study Time by Subject Chart -->
                    <div class="bg-white dark:bg-slate-900 p-5 sm:p-6 rounded-3xl border border-slate-200 dark:border-slate-800 flex flex-col">
                        <div class="flex items-center justify-between mb-4">
                            <div>
                                <h3 class="text-sm font-bold text-slate-900 dark:text-white">Study Time by Subject</h3>
                                <p class="text-xs text-slate-500 dark:text-slate-400">Minutes invested per topic</p>
                            </div>
                            <span class="w-8 h-8 rounded-xl bg-indigo-50 dark:bg-indigo-500/10 text-indigo-600 dark:text-indigo-400 flex items-center justify-center text-xs">
                                <i class="fa-solid fa-chart-pie"></i>
                            </span>
                        </div>
                        <div class="relative flex-1 min-h-[210px] flex items-center justify-center">
                            <canvas id="subjectChart"></canvas>
                            <div id="subject-chart-empty" class="hidden absolute inset-0 flex flex-col items-center justify-center text-slate-400 text-xs text-center p-4">
                                <i class="fa-solid fa-chart-simple text-2xl mb-2 opacity-40"></i>
                                Complete a study session to visualize subject distribution
                            </div>
                        </div>
                    </div>

                    <!-- Distraction Breakdown Chart -->
                    <div class="bg-white dark:bg-slate-900 p-5 sm:p-6 rounded-3xl border border-slate-200 dark:border-slate-800 flex flex-col">
                        <div class="flex items-center justify-between mb-4">
                            <div>
                                <h3 class="text-sm font-bold text-slate-900 dark:text-white">Distraction Triggers</h3>
                                <p class="text-xs text-slate-500 dark:text-slate-400">Frequency by interruption type</p>
                            </div>
                            <span class="w-8 h-8 rounded-xl bg-amber-50 dark:bg-amber-500/10 text-amber-600 dark:text-amber-400 flex items-center justify-center text-xs">
                                <i class="fa-solid fa-chart-bar"></i>
                            </span>
                        </div>
                        <div class="relative flex-1 min-h-[210px] flex items-center justify-center">
                            <canvas id="distractionChart"></canvas>
                            <div id="distraction-chart-empty" class="hidden absolute inset-0 flex flex-col items-center justify-center text-slate-400 text-xs text-center p-4">
                                <i class="fa-solid fa-shield-halved text-2xl mb-2 opacity-40"></i>
                                No distractions recorded yet
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Session History Table -->
                <div class="bg-white dark:bg-slate-900 rounded-3xl border border-slate-200 dark:border-slate-800 overflow-hidden flex-1 flex flex-col">
                    <div class="p-5 sm:p-6 border-b border-slate-100 dark:border-slate-800 flex items-center justify-between">
                        <div>
                            <h3 class="text-base font-bold text-slate-900 dark:text-white">Session History</h3>
                            <p class="text-xs text-slate-500 dark:text-slate-400">Your recent completed focus blocks</p>
                        </div>
                        <span id="history-count-badge" class="text-xs font-medium px-2.5 py-1 rounded-lg bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300">
                            0 entries
                        </span>
                    </div>

                    <div class="overflow-x-auto flex-1">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="border-b border-slate-100 dark:border-slate-800/80 text-[11px] font-semibold uppercase tracking-wider text-slate-400 bg-slate-50/50 dark:bg-slate-850/50">
                                    <th class="py-3 px-5">Subject</th>
                                    <th class="py-3 px-4">Duration</th>
                                    <th class="py-3 px-4">Distractions</th>
                                    <th class="py-3 px-5 text-right">Completed At</th>
                                </tr>
                            </thead>
                            <tbody id="session-history-body" class="divide-y divide-slate-100 dark:divide-slate-800/60 text-sm">
                                <!-- Populated dynamically -->
                            </tbody>
                        </table>
                        
                        <!-- Empty State -->
                        <div id="history-empty-state" class="py-12 px-4 text-center">
                            <div class="w-12 h-12 rounded-2xl bg-slate-100 dark:bg-slate-800 text-slate-400 flex items-center justify-center mx-auto mb-3">
                                <i class="fa-solid fa-hourglass-start text-lg"></i>
                            </div>
                            <p class="text-sm font-medium text-slate-700 dark:text-slate-300">No study sessions recorded yet</p>
                            <p class="text-xs text-slate-500 dark:text-slate-400 mt-1 max-w-xs mx-auto">Start the Pomodoro timer on the left or click "Demo Data" at the top to explore analytics.</p>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </main>

    <!-- Application Logic -->
    <script>
        /**
         * STATE & STORAGE MANAGEMENT
         */
        const STORAGE_KEY = 'focusflow_study_tracker_v1';
        const DEFAULT_SUBJECTS = ['Mathematics', 'Physics', 'Coding', 'History', 'Literature'];

        let appState = {
            subjects: [...DEFAULT_SUBJECTS],
            selectedSubject: 'Mathematics',
            studyDuration: 25, // minutes
            breakDuration: 5,  // minutes
            sessions: [],      // { id, subject, durationMins, distractionsCount, timestamp }
            distractions: [],  // { id, type, subject, timestamp }
            theme: 'dark'
        };

        // Active Timer Runtime Variables
        let timerMode = 'study'; // 'study' | 'break'
        let timeLeftSeconds = 25 * 60;
        let totalModeSeconds = 25 * 60;
        let timerInterval = null;
        let isRunning = false;
        let currentSessionDistractions = 0;

        // Chart Instances
        let subjectChartInstance = null;
        let distractionChartInstance = null;

        /**
         * INITIALIZATION
         */
        window.addEventListener('DOMContentLoaded', () => {
            loadState();
            applyTheme(appState.theme);
            renderSubjectsDropdown();
            
            // Sync inputs with loaded state
            document.getElementById('study-duration-input').value = appState.studyDuration;
            document.getElementById('break-duration-input').value = appState.breakDuration;
            
            resetTimer(false);
            updateAllAnalytics();
        });

        function loadState() {
            try {
                const raw = localStorage.getItem(STORAGE_KEY);
                if (raw) {
                    const parsed = JSON.parse(raw);
                    appState = { ...appState, ...parsed };
                }
            } catch (e) {
                console.error('Failed to load state from LocalStorage:', e);
            }
        }

        function saveState() {
            try {
                localStorage.setItem(STORAGE_KEY, JSON.stringify(appState));
            } catch (e) {
                console.error('Failed to save state:', e);
            }
        }

        /**
         * WEB AUDIO API CHIME GENERATOR
         * Creates a pleasant, gentle harmonic chime without external audio files
         */
        function playCompletionChime() {
            try {
                const AudioContext = window.AudioContext || window.webkitAudioContext;
                const ctx = new AudioContext();
                const now = ctx.currentTime;

                // Harmonic chord notes (C5, E5, G5, B5)
                const frequencies = [523.25, 659.25, 783.99, 987.77];

                frequencies.forEach((freq, idx) => {
                    const osc = ctx.createOscillator();
                    const gain = ctx.createGain();

                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(freq, now + idx * 0.12);

                    gain.gain.setValueAtTime(0.001, now + idx * 0.12);
                    gain.gain.exponentialRampToValueAtTime(0.12, now + idx * 0.12 + 0.05);
                    gain.gain.exponentialRampToValueAtTime(0.0001, now + idx * 0.12 + 1.4);

                    osc.connect(gain);
                    gain.connect(ctx.destination);

                    osc.start(now + idx * 0.12);
                    osc.stop(now + idx * 0.12 + 1.5);
                });
            } catch (err) {
                console.warn('Web Audio API blocked or unsupported:', err);
            }
        }

        /**
         * POMODORO TIMER LOGIC
         */
        function switchMode(newMode) {
            if (isRunning) {
                pauseTimer();
            }
            timerMode = newMode;

            const studyBtn = document.getElementById('mode-study');
            const breakBtn = document.getElementById('mode-break');
            const ring = document.getElementById('timer-ring');
            const glow = document.getElementById('timer-glow');
            const badge = document.getElementById('timer-status-badge');
            const subjectSection = document.getElementById('subject-section');

            if (newMode === 'study') {
                studyBtn.className = "flex-1 py-2.5 px-4 rounded-xl text-sm font-semibold transition-all bg-white dark:bg-indigo-600 text-indigo-600 dark:text-white shadow-sm";
                breakBtn.className = "flex-1 py-2.5 px-4 rounded-xl text-sm font-semibold transition-all text-slate-600 dark:text-slate-400 hover:text-slate-900 dark:hover:text-white";
                
                ring.classList.remove('text-emerald-500');
                ring.classList.add('text-indigo-600', 'dark:text-indigo-500');
                glow.className = "absolute -top-24 -right-24 w-48 h-48 bg-indigo-500/10 rounded-full blur-3xl pointer-events-none transition-colors duration-500";
                badge.className = "text-xs font-semibold uppercase tracking-widest text-indigo-600 dark:text-indigo-400 mb-1";
                subjectSection.classList.remove('opacity-50', 'pointer-events-none');
            } else {
                breakBtn.className = "flex-1 py-2.5 px-4 rounded-xl text-sm font-semibold transition-all bg-white dark:bg-emerald-600 text-emerald-600 dark:text-white shadow-sm";
                studyBtn.className = "flex-1 py-2.5 px-4 rounded-xl text-sm font-semibold transition-all text-slate-600 dark:text-slate-400 hover:text-slate-900 dark:hover:text-white";
                
                ring.classList.remove('text-indigo-600', 'dark:text-indigo-500');
                ring.classList.add('text-emerald-500');
                glow.className = "absolute -top-24 -right-24 w-48 h-48 bg-emerald-500/10 rounded-full blur-3xl pointer-events-none transition-colors duration-500";
                badge.className = "text-xs font-semibold uppercase tracking-widest text-emerald-600 dark:text-emerald-400 mb-1";
                subjectSection.classList.add('opacity-50', 'pointer-events-none');
            }

            resetTimer(false);
        }

        function updateCustomDurations() {
            const studyInput = parseInt(document.getElementById('study-duration-input').value, 10);
            const breakInput = parseInt(document.getElementById('break-duration-input').value, 10);

            if (studyInput >= 1 && studyInput <= 180) {
                appState.studyDuration = studyInput;
            }
            if (breakInput >= 1 && breakInput <= 60) {
                appState.breakDuration = breakInput;
            }
            saveState();

            if (!isRunning) {
                resetTimer(false);
            }
        }

        function toggleTimer() {
            if (isRunning) {
                pauseTimer();
            } else {
                startTimer();
            }
        }

        function startTimer() {
            if (isRunning) return;
            isRunning = true;

            const btn = document.getElementById('btn-start-pause');
            const icon = document.getElementById('start-pause-icon');
            const text = document.getElementById('start-pause-text');
            const badge = document.getElementById('timer-status-badge');

            icon.className = 'fa-solid fa-pause';
            text.textContent = 'Pause';
            badge.textContent = timerMode === 'study' ? 'Focusing...' : 'Resting...';

            if (timerMode === 'study') {
                btn.classList.replace('bg-indigo-600', 'bg-amber-600');
                btn.classList.replace('hover:bg-indigo-700', 'hover:bg-amber-700');
            }

            timerInterval = setInterval(() => {
                if (timeLeftSeconds > 0) {
                    timeLeftSeconds--;
                    updateTimerDisplay();
                } else {
                    handleTimerComplete();
                }
            }, 1000);
        }

        function pauseTimer() {
            isRunning = false;
            clearInterval(timerInterval);

            const btn = document.getElementById('btn-start-pause');
            const icon = document.getElementById('start-pause-icon');
            const text = document.getElementById('start-pause-text');
            const badge = document.getElementById('timer-status-badge');

            icon.className = 'fa-solid fa-play';
            text.textContent = 'Resume';
            badge.textContent = 'Paused';

            btn.classList.replace('bg-amber-600', 'bg-indigo-600');
            btn.classList.replace('hover:bg-amber-700', 'hover:bg-indigo-700');
        }

        function resetTimer(showToastMsg = false) {
            isRunning = false;
            clearInterval(timerInterval);

            const mins = timerMode === 'study' ? appState.studyDuration : appState.breakDuration;
            totalModeSeconds = mins * 60;
            timeLeftSeconds = totalModeSeconds;

            const btn = document.getElementById('btn-start-pause');
            const icon = document.getElementById('start-pause-icon');
            const text = document.getElementById('start-pause-text');
            const badge = document.getElementById('timer-status-badge');

            icon.className = 'fa-solid fa-play';
            text.textContent = 'Start';
            badge.textContent = 'Ready';
            btn.classList.replace('bg-amber-600', 'bg-indigo-600');
            btn.classList.replace('hover:bg-amber-700', 'hover:bg-indigo-700');

            updateTimerDisplay();
            if (showToastMsg) showToast('Timer reset', 'info');
        }

        function updateTimerDisplay() {
            const mins = Math.floor(timeLeftSeconds / 60);
            const secs = timeLeftSeconds % 60;
            const formatted = `${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
            
            document.getElementById('timer-display').textContent = formatted;
            document.title = `${formatted} • FocusFlow`;

            // Update SVG circle stroke offset (Circumference = 2 * pi * 44 ≈ 276.46)
            const circumference = 276.46;
            const progress = totalModeSeconds > 0 ? timeLeftSeconds / totalModeSeconds : 1;
            const offset = circumference * (1 - progress);
            document.getElementById('timer-ring').style.strokeDashoffset = offset;
        }

        function handleTimerComplete() {
            pauseTimer();
            playCompletionChime();

            if (timerMode === 'study') {
                recordStudySession(appState.studyDuration);
                showToast(`Great job! ${appState.studyDuration}m of ${appState.selectedSubject} logged.`, 'success');
                switchMode('break');
            } else {
                showToast('Break finished! Ready for another focus block?', 'info');
                switchMode('study');
            }
        }

        function completeSessionEarly() {
            if (timerMode !== 'study') {
                switchMode('study');
                return;
            }
            const elapsedSeconds = totalModeSeconds - timeLeftSeconds;
            const elapsedMins = Math.max(1, Math.round(elapsedSeconds / 60));
            
            pauseTimer();
            playCompletionChime();
            recordStudySession(elapsedMins);
            showToast(`Logged ${elapsedMins}m session for ${appState.selectedSubject}!`, 'success');
            resetTimer(false);
        }

        function recordStudySession(durationMins) {
            const newSession = {
                id: Date.now(),
                subject: appState.selectedSubject,
                durationMins: durationMins,
                distractionsCount: currentSessionDistractions,
                timestamp: new Date().toISOString()
            };

            appState.sessions.unshift(newSession);
            currentSessionDistractions = 0;
            updateCurrentDistractionCounter();
            saveState();
            updateAllAnalytics();
        }

        /**
         * SUBJECT TAGGING MANAGEMENT
         */
        function renderSubjectsDropdown() {
            const select = document.getElementById('subject-select');
            select.innerHTML = '';

            appState.subjects.forEach(subj => {
                const opt = document.createElement('option');
                opt.value = subj;
                opt.textContent = subj;
                if (subj === appState.selectedSubject) opt.selected = true;
                select.appendChild(opt);
            });

            document.getElementById('active-subject-label').textContent = appState.selectedSubject;

            select.onchange = (e) => {
                appState.selectedSubject = e.target.value;
                document.getElementById('active-subject-label').textContent = appState.selectedSubject;
                saveState();
            };
        }

        function toggleNewSubjectInput() {
            const box = document.getElementById('new-subject-box');
            box.classList.toggle('hidden');
            if (!box.classList.contains('hidden')) {
                document.getElementById('new-subject-input').focus();
            }
        }

        function addNewSubject() {
            const input = document.getElementById('new-subject-input');
            const val = input.value.trim();
            if (!val) return;

            if (!appState.subjects.some(s => s.toLowerCase() === val.toLowerCase())) {
                appState.subjects.push(val);
            }
            appState.selectedSubject = val;
            input.value = '';
            document.getElementById('new-subject-box').classList.add('hidden');
            
            saveState();
            renderSubjectsDropdown();
            showToast(`Subject "${val}" selected`, 'success');
        }

        /**
         * DISTRACTION LOGGER
         */
        function logDistraction(type) {
            const entry = {
                id: Date.now(),
                type: type,
                subject: appState.selectedSubject,
                timestamp: new Date().toISOString()
            };

            appState.distractions.unshift(entry);
            currentSessionDistractions++;
            
            saveState();
            updateCurrentDistractionCounter();
            updateAllAnalytics();
            showToast(`Logged distraction: ${type}`, 'warning');
        }

        function updateCurrentDistractionCounter() {
            document.getElementById('current-session-distractions').textContent = `Current session: ${currentSessionDistractions}`;
            
            // Count today's distractions
            const todayStr = new Date().toDateString();
            const todayCount = appState.distractions.filter(d => new Date(d.timestamp).toDateString() === todayStr).length;
            document.getElementById('session-distraction-badge').textContent = `${todayCount} logged today`;
        }

        /**
         * ANALYTICS DASHBOARD & CHARTS
         */
        function updateAllAnalytics() {
            updateCurrentDistractionCounter();
            renderDistractionFeed();
            updateKPICards();
            renderHistoryTable();
            renderCharts();
        }

        function renderDistractionFeed() {
            const feed = document.getElementById('distraction-feed');
            if (appState.distractions.length === 0) {
                feed.innerHTML = `<p class="text-slate-400 italic py-2 text-center">No distractions logged yet. Stay sharp!</p>`;
                return;
            }

            feed.innerHTML = appState.distractions.slice(0, 6).map(d => {
                const time = new Date(d.timestamp).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
                return `
                    <div class="flex items-center justify-between py-1 px-2 rounded-lg bg-white dark:bg-slate-900/80 border border-slate-100 dark:border-slate-800">
                        <span class="font-medium text-slate-700 dark:text-slate-300 truncate pr-2">${escapeHTML(d.type)}</span>
                        <span class="text-[10px] text-slate-400 shrink-0">${escapeHTML(d.subject)} • ${time}</span>
                    </div>
                `;
            }).join('');
        }

        function updateKPICards() {
            const totalMins = appState.sessions.reduce((acc, s) => acc + s.durationMins, 0);
            const hours = Math.floor(totalMins / 60);
            const mins = totalMins % 60;
            document.getElementById('kpi-total-time').textContent = hours > 0 ? `${hours}h ${mins}m` : `${mins}m`;

            document.getElementById('kpi-total-sessions').textContent = appState.sessions.length;
            document.getElementById('kpi-total-distractions').textContent = appState.distractions.length;

            // Top Subject calculation
            if (appState.sessions.length > 0) {
                const subjectTotals = {};
                appState.sessions.forEach(s => {
                    subjectTotals[s.subject] = (subjectTotals[s.subject] || 0) + s.durationMins;
                });
                const topSubj = Object.entries(subjectTotals).sort((a, b) => b[1] - a[1])[0];
                document.getElementById('kpi-top-subject').textContent = topSubj[0];
                document.getElementById('kpi-top-subject-sub').textContent = `${topSubj[1]} mins focused`;
            } else {
                document.getElementById('kpi-top-subject').textContent = '—';
                document.getElementById('kpi-top-subject-sub').textContent = 'No data yet';
            }

            // Top Distraction calculation
            if (appState.distractions.length > 0) {
                const distTotals = {};
                appState.distractions.forEach(d => {
                    distTotals[d.type] = (distTotals[d.type] || 0) + 1;
                });
                const topDist = Object.entries(distTotals).sort((a, b) => b[1] - a[1])[0];
                document.getElementById('kpi-top-distraction').textContent = `Top: ${topDist[0].split('/')[0].trim()}`;
            } else {
                document.getElementById('kpi-top-distraction').textContent = 'Clear mind';
            }
        }

        function renderHistoryTable() {
            const tbody = document.getElementById('session-history-body');
            const emptyState = document.getElementById('history-empty-state');
            const badge = document.getElementById('history-count-badge');

            badge.textContent = `${appState.sessions.length} ${appState.sessions.length === 1 ? 'entry' : 'entries'}`;

            if (appState.sessions.length === 0) {
                tbody.innerHTML = '';
                emptyState.classList.remove('hidden');
                return;
            }

            emptyState.classList.add('hidden');
            tbody.innerHTML = appState.sessions.slice(0, 15).map(session => {
                const dateObj = new Date(session.timestamp);
                const dateStr = dateObj.toLocaleDateString([], { month: 'short', day: 'numeric' });
                const timeStr = dateObj.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });

                const distBadge = session.distractionsCount === 0
                    ? `<span class="inline-flex items-center gap-1 px-2 py-0.5 rounded-md text-xs font-medium bg-emerald-50 text-emerald-700 dark:bg-emerald-500/10 dark:text-emerald-400"><i class="fa-solid fa-check text-[10px]"></i> 0</span>`
                    : `<span class="inline-flex items-center gap-1 px-2 py-0.5 rounded-md text-xs font-medium bg-amber-50 text-amber-700 dark:bg-amber-500/10 dark:text-amber-400"><i class="fa-solid fa-bolt text-[10px]"></i> ${session.distractionsCount}</span>`;

                return `
                    <tr class="hover:bg-slate-50/80 dark:hover:bg-slate-850/60 transition">
                        <td class="py-3.5 px-5 font-medium text-slate-900 dark:text-slate-200">${escapeHTML(session.subject)}</td>
                        <td class="py-3.5 px-4 font-mono text-xs text-indigo-600 dark:text-indigo-400 font-semibold">${session.durationMins} mins</td>
                        <td class="py-3.5 px-4">${distBadge}</td>
                        <td class="py-3.5 px-5 text-right text-xs text-slate-500 dark:text-slate-400">${dateStr}, ${timeStr}</td>
                    </tr>
                `;
            }).join('');
        }

        function renderCharts() {
            const isDark = appState.theme === 'dark';
            const textColor = isDark ? '#94a3b8' : '#64748b';
            const gridColor = isDark ? 'rgba(51, 65, 85, 0.4)' : 'rgba(226, 232, 240, 0.8)';

            // 1. SUBJECT DOUGHNUT CHART
            const subjectEmpty = document.getElementById('subject-chart-empty');
            const subjectCanvas = document.getElementById('subjectChart');

            if (appState.sessions.length === 0) {
                subjectEmpty.classList.remove('hidden');
                subjectCanvas.classList.add('opacity-0');
            } else {
                subjectEmpty.classList.add('hidden');
                subjectCanvas.classList.remove('opacity-0');

                const subjectMap = {};
                appState.sessions.forEach(s => {
                    subjectMap[s.subject] = (subjectMap[s.subject] || 0) + s.durationMins;
                });

                const labels = Object.keys(subjectMap);
                const data = Object.values(subjectMap);
                const palette = ['#6366f1', '#10b981', '#f59e0b', '#ec4899', '#06b6d4', '#8b5cf6', '#f43f5e'];

                if (subjectChartInstance) subjectChartInstance.destroy();
                subjectChartInstance = new Chart(subjectCanvas, {
                    type: 'doughnut',
                    data: {
                        labels: labels,
                        datasets: [{
                            data: data,
                            backgroundColor: palette.slice(0, labels.length),
                            borderWidth: isDark ? 2 : 2,
                            borderColor: isDark ? '#0f172a' : '#ffffff',
                            hoverOffset: 6
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        cutout: '68%',
                        plugins: {
                            legend: {
                                position: 'right',
                                labels: {
                                    color: textColor,
                                    usePointStyle: true,
                                    pointStyle: 'circle',
                                    padding: 14,
                                    font: { family: 'Inter', size: 11 }
                                }
                            },
                            tooltip: {
                                callbacks: {
                                    label: (ctx) => ` ${ctx.label}: ${ctx.raw} mins`
                                }
                            }
                        }
                    }
                });
            }

            // 2. DISTRACTION BAR CHART
            const distEmpty = document.getElementById('distraction-chart-empty');
            const distCanvas = document.getElementById('distractionChart');

            if (appState.distractions.length === 0) {
                distEmpty.classList.remove('hidden');
                distCanvas.classList.add('opacity-0');
            } else {
                distEmpty.classList.add('hidden');
                distCanvas.classList.remove('opacity-0');

                const distMap = {};
                appState.distractions.forEach(d => {
                    const shortLabel = d.type.split('/')[0].trim();
                    distMap[shortLabel] = (distMap[shortLabel] || 0) + 1;
                });

                const labels = Object.keys(distMap);
                const data = Object.values(distMap);

                if (distractionChartInstance) distractionChartInstance.destroy();
                distractionChartInstance = new Chart(distCanvas, {
                    type: 'bar',
                    data: {
                        labels: labels,
                        datasets: [{
                            label: 'Count',
                            data: data,
                            backgroundColor: 'rgba(245, 158, 11, 0.85)',
                            borderRadius: 8,
                            barThickness: 26
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { display: false }
                        },
                        scales: {
                            y: {
                                beginAtZero: true,
                                ticks: { stepSize: 1, color: textColor, font: { size: 11 } },
                                grid: { color: gridColor }
                            },
                            x: {
                                ticks: { color: textColor, font: { size: 11 } },
                                grid: { display: false }
                            }
                        }
                    }
                });
            }
        }

        /**
         * DEMO DATA & RESET CONTROLS
         */
        function loadDemoData() {
            const now = Date.now();
            const hour = 3600 * 1000;

            appState.sessions = [
                { id: 1, subject: 'Coding', durationMins: 50, distractionsCount: 1, timestamp: new Date(now - 1 * hour).toISOString() },
                { id: 2, subject: 'Mathematics', durationMins: 25, distractionsCount: 0, timestamp: new Date(now - 3 * hour).toISOString() },
                { id: 3, subject: 'Physics', durationMins: 45, distractionsCount: 2, timestamp: new Date(now - 5 * hour).toISOString() },
                { id: 4, subject: 'Coding', durationMins: 25, distractionsCount: 0, timestamp: new Date(now - 24 * hour).toISOString() },
                { id: 5, subject: 'History', durationMins: 30, distractionsCount: 1, timestamp: new Date(now - 26 * hour).toISOString() },
                { id: 6, subject: 'Literature', durationMins: 25, distractionsCount: 0, timestamp: new Date(now - 48 * hour).toISOString() }
            ];

            appState.distractions = [
                { id: 101, type: 'Phone / Notifications', subject: 'Coding', timestamp: new Date(now - 1.2 * hour).toISOString() },
                { id: 102, type: 'Fatigue / Daydreaming', subject: 'Physics', timestamp: new Date(now - 5.1 * hour).toISOString() },
                { id: 103, type: 'Phone / Notifications', subject: 'Physics', timestamp: new Date(now - 5.3 * hour).toISOString() },
                { id: 104, type: 'Social Media / Web', subject: 'History', timestamp: new Date(now - 26.2 * hour).toISOString() },
                { id: 105, type: 'Environment / Noise', subject: 'Coding', timestamp: new Date(now - 28 * hour).toISOString() }
            ];

            saveState();
            updateAllAnalytics();
            showToast('Sample study analytics loaded!', 'success');
        }

        function promptClearData() {
            showModal(
                'Reset All Study Data?',
                'This will permanently clear your session history, distraction logs, and custom subjects from this browser.',
                () => {
                    appState.subjects = [...DEFAULT_SUBJECTS];
                    appState.selectedSubject = 'Mathematics';
                    appState.sessions = [];
                    appState.distractions = [];
                    currentSessionDistractions = 0;

                    if (subjectChartInstance) {
                        subjectChartInstance.destroy();
                        subjectChartInstance = null;
                    }
                    if (distractionChartInstance) {
                        distractionChartInstance.destroy();
                        distractionChartInstance = null;
                    }

                    saveState();
                    renderSubjectsDropdown();
                    updateAllAnalytics();
                    showToast('All data has been cleared.', 'info');
                }
            );
        }

        /**
         * THEME TOGGLE
         */
        document.getElementById('theme-toggle').addEventListener('click', () => {
            appState.theme = appState.theme === 'dark' ? 'light' : 'dark';
            applyTheme(appState.theme);
            saveState();
            renderCharts(); // Refresh chart label colors
        });

        function applyTheme(theme) {
            const html = document.documentElement;
            const icon = document.getElementById('theme-icon');
            if (theme === 'dark') {
                html.classList.add('dark');
                icon.className = 'fa-solid fa-sun text-amber-400';
            } else {
                html.classList.remove('dark');
                icon.className = 'fa-solid fa-moon text-slate-600';
            }
        }

        /**
         * UI UTILITIES: TOASTS, MODALS & SANITIZATION
         */
        function showToast(message, type = 'info') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            
            const styles = {
                success: 'bg-emerald-600 text-white',
                warning: 'bg-amber-600 text-white',
                info: 'bg-slate-800 dark:bg-slate-700 text-white'
            };

            const icons = {
                success: 'fa-circle-check',
                warning: 'fa-bolt',
                info: 'fa-circle-info'
            };

            toast.className = `${styles[type] || styles.info} px-4 py-3 rounded-2xl shadow-xl flex items-center gap-2.5 text-sm font-medium transform translate-y-4 opacity-0 transition-all duration-300 pointer-events-auto`;
            toast.innerHTML = `<i class="fa-solid ${icons[type] || icons.info}"></i><span>${escapeHTML(message)}</span>`;

            container.appendChild(toast);

            requestAnimationFrame(() => {
                toast.classList.remove('translate-y-4', 'opacity-0');
            });

            setTimeout(() => {
                toast.classList.add('translate-y-4', 'opacity-0');
                setTimeout(() => toast.remove(), 300);
            }, 3200);
        }

        function showModal(title, message, onConfirm) {
            const modal = document.getElementById('confirm-modal');
            document.getElementById('modal-title').textContent = title;
            document.getElementById('modal-message').textContent = message;

            modal.classList.remove('hidden');
            modal.classList.add('flex');

            const close = () => {
                modal.classList.add('hidden');
                modal.classList.remove('flex');
            };

            document.getElementById('modal-cancel').onclick = close;
            document.getElementById('modal-confirm').onclick = () => {
                close();
                onConfirm();
            };
        }

        function escapeHTML(str) {
            return String(str)
                .replace(/&/g, '&amp;')
                .replace(/</g, '&lt;')
                .replace(/>/g, '&gt;')
                .replace(/"/g, '&quot;');
        }
    </script>
</body>
</html>
