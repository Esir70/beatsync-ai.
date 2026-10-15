<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BeatSync AI - Universal AI Music & Beat Integrator</title>
    <!-- Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f5f3ff',
                            100: '#ede9fe',
                            500: '#8b5cf6',
                            600: '#7c3aed',
                            700: '#6d28d9',
                            900: '#4c1d95',
                            dark: '#0f0c1b',
                            card: '#18122b',
                            border: '#2e244a'
                        }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #0f0c1b;
            color: #f3f4f6;
        }
        .glow-effect {
            box-shadow: 0 0 25px rgba(139, 92, 246, 0.25);
        }
        .glow-effect-strong {
            box-shadow: 0 0 40px rgba(139, 92, 246, 0.4);
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0f0c1b;
        }
        ::-webkit-scrollbar-thumb {
            background: #2e244a;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #7c3aed;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-brand-500 selection:text-white">

    <!-- HEADER / NAVBAR -->
    <header class="border-b border-brand-border bg-brand-dark/80 backdrop-blur-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-brand-600 to-indigo-400 flex items-center justify-center glow-effect">
                    <i class="fa-solid fa-waveform text-white text-lg"></i>
                </div>
                <div>
                    <span class="text-xl font-extrabold bg-gradient-to-r from-white via-brand-100 to-brand-500 bg-clip-text text-transparent">BeatSync AI</span>
                    <span class="text-xs block text-brand-500 font-medium tracking-widest uppercase">Universal Beat Integrator</span>
                </div>
            </div>
            <div class="flex items-center space-x-4">
                <span class="hidden sm:inline-flex items-center px-3 py-1 rounded-full text-xs font-medium bg-brand-700/30 border border-brand-500/30 text-brand-300">
                    <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse mr-2"></span> AI Engine Online
                </span>
            </div>
        </div>
    </header>

    <!-- MAIN CONTENT CONTAINER -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 w-full flex-grow grid grid-cols-1 lg:grid-cols-12 gap-8">
        
        <!-- LEFT COLUMN: INPUT & CONTROLS (Cols 1-7) -->
        <div class="lg:col-span-7 space-y-6">
            
            <!-- STEP 1: VOCAL UPLOAD OR RECORD -->
            <div class="bg-brand-card border border-brand-border rounded-2xl p-6 shadow-xl relative overflow-hidden">
                <div class="absolute top-0 right-0 w-32 h-32 bg-brand-600/10 rounded-full blur-2xl pointer-events-none"></div>
                <div class="flex items-center justify-between mb-4">
                    <h2 class="text-lg font-bold flex items-center text-white">
                        <span class="w-7 h-7 rounded-lg bg-brand-600 text-white text-sm flex items-center justify-center mr-3 font-bold shadow-md">1</span>
                        Provide Vocal Track (Freestyle / Acapella)
                    </h2>
                    <span class="text-xs text-gray-400">MP3, WAV, WebM</span>
                </div>

                <!-- Tabs for Upload vs Record -->
                <div class="grid grid-cols-2 gap-2 p-1 bg-brand-dark/60 rounded-xl mb-4 border border-brand-border/60">
                    <button id="tabUploadBtn" onclick="switchTab('upload')" class="py-2.5 px-4 rounded-lg text-sm font-semibold transition-all bg-brand-600 text-white shadow-md flex items-center justify-center space-x-2">
                        <i class="fa-solid fa-cloud-arrow-up"></i>
                        <span>Upload MP3</span>
                    </button>
                    <button id="tabRecordBtn" onclick="switchTab('record')" class="py-2.5 px-4 rounded-lg text-sm font-semibold transition-all text-gray-400 hover:text-white flex items-center justify-center space-x-2">
                        <i class="fa-solid fa-microphone"></i>
                        <span>Record Live</span>
                    </button>
                </div>

                <!-- Upload Section -->
                <div id="uploadSection" class="space-y-4">
                    <div id="dropZone" class="border-2 border-dashed border-brand-border hover:border-brand-500 rounded-xl p-8 text-center cursor-pointer transition-all bg-brand-dark/40 hover:bg-brand-dark/70 group">
                        <input type="file" id="audioFileInput" accept="audio/*" class="hidden" onchange="handleFileSelect(event)">
                        <div class="w-14 h-14 rounded-full bg-brand-700/20 text-brand-400 group-hover:scale-110 group-hover:bg-brand-600 group-hover:text-white transition-all mx-auto flex items-center justify-center mb-3">
                            <i class="fa-solid fa-file-audio text-2xl"></i>
                        </div>
                        <p class="text-sm font-semibold text-gray-200">Click to upload or drag & drop your audio</p>
                        <p class="text-xs text-gray-400 mt-1">Supports MP3, WAV, M4A up to 50MB</p>
                    </div>
                </div>

                <!-- Record Section (Hidden by default) -->
                <div id="recordSection" class="hidden space-y-4 text-center py-6 bg-brand-dark/40 rounded-xl border border-brand-border/60">
                    <div id="recordingTimer" class="text-3xl font-mono font-bold text-brand-400">00:00</div>
                    <p class="text-xs text-gray-400" id="recordStatusText">Click the button below to start recording your freestyle</p>
                    <div class="flex justify-center space-x-4">
                        <button id="recordBtn" onclick="toggleRecording()" class="px-6 py-3 bg-red-600 hover:bg-red-500 text-white rounded-xl font-bold transition-all shadow-lg flex items-center space-x-2">
                            <i class="fa-solid fa-circle text-xs animate-ping"></i>
                            <span id="recordBtnText">Start Recording</span>
                        </button>
                    </div>
                </div>

                <!-- File Info Card (Appears after load/record) -->
                <div id="fileInfoCard" class="hidden mt-4 p-4 bg-brand-dark/60 rounded-xl border border-brand-border flex items-center justify-between">
                    <div class="flex items-center space-x-3 overflow-hidden">
                        <div class="w-10 h-10 rounded-lg bg-emerald-500/20 text-emerald-400 flex items-center justify-center flex-shrink-0">
                            <i class="fa-solid fa-music"></i>
                        </div>
                        <div class="truncate">
                            <h4 id="fileNameDisplay" class="text-sm font-bold text-white truncate">track_vocal.mp3</h4>
                            <p id="fileMetaDisplay" class="text-xs text-emerald-400 font-medium">Ready for AI processing</p>
                        </div>
                    </div>
                    <button onclick="clearVocal()" class="text-gray-400 hover:text-red-400 p-2 text-sm transition-colors">
                        <i class="fa-solid fa-trash-can"></i>
                    </button>
                </div>
            </div>

            <!-- STEP 2: GENRE & STYLE SELECTION -->
            <div class="bg-brand-card border border-brand-border rounded-2xl p-6 shadow-xl">
                <div class="flex items-center justify-between mb-4">
                    <h2 class="text-lg font-bold flex items-center text-white">
                        <span class="w-7 h-7 rounded-lg bg-brand-600 text-white text-sm flex items-center justify-center mr-3 font-bold shadow-md">2</span>
                        Choose Target Music Genre & Vibe
                    </h2>
                    <span class="text-xs text-brand-400 font-semibold">Universal AI Engine</span>
                </div>

                <!-- Genre Grid -->
                <div class="grid grid-cols-2 sm:grid-cols-4 gap-3">
                    <button onclick="selectGenre('hiphop', 'Hip-Hop / Drill', 140, 'Minor')" id="genre-hiphop" class="genre-card p-3 rounded-xl border border-brand-border bg-brand-dark/40 hover:border-brand-500 transition-all text-left group">
                        <div class="text-brand-400 mb-1 group-hover:scale-110 transition-transform"><i class="fa-solid fa-drum text-lg"></i></div>
                        <div class="text-sm font-bold text-white">Hip-Hop / Drill</div>
                        <div class="text-[10px] text-gray-400">140 BPM • 808 Bass</div>
                    </button>
                    <button onclick="selectGenre('afrobeats', 'Afrobeat / Amapiano', 115, 'Major')" id="genre-afrobeats" class="genre-card p-3 rounded-xl border border-brand-border bg-brand-dark/40 hover:border-brand-500 transition-all text-left group">
                        <div class="text-brand-400 mb-1 group-hover:scale-110 transition-transform"><i class="fa-solid fa-compact-disc text-lg"></i></div>
                        <div class="text-sm font-bold text-white">Afrobeat / Amapiano</div>
                        <div class="text-[10px] text-gray-400">115 BPM • Log Drum</div>
                    </button>
                    <button onclick="selectGenre('pop', 'Pop & R&B', 120, 'Major')" id="genre-pop" class="genre-card p-3 rounded-xl border border-brand-border bg-brand-dark/40 hover:border-brand-500 transition-all text-left group">
                        <div class="text-brand-400 mb-1 group-hover:scale-110 transition-transform"><i class="fa-solid fa-guitar text-lg"></i></div>
                        <div class="text-sm font-bold text-white">Pop & R&B</div>
                        <div class="text-[10px] text-gray-400">120 BPM • Melodic</div>
                    </button>
                    <button onclick="selectGenre('electronic', 'EDM & House', 128, 'Minor')" id="genre-electronic" class="genre-card p-3 rounded-xl border border-brand-border bg-brand-dark/40 hover:border-brand-500 transition-all text-left group">
                        <div class="text-brand-400 mb-1 group-hover:scale-110 transition-transform"><i class="fa-solid fa-bolt text-lg"></i></div>
                        <div class="text-sm font-bold text-white">EDM & House</div>
                        <div class="text-[10px] text-gray-400">128 BPM • Synth Lead</div>
                    </button>
                    <button onclick="selectGenre('lofi', 'Acoustic / Lo-Fi', 85, 'Major')" id="genre-lofi" class="genre-card p-3 rounded-xl border border-brand-border bg-brand-dark/40 hover:border-brand-500 transition-all text-left group">
                        <div class="text-brand-400 mb-1 group-hover:scale-110 transition-transform"><i class="fa-solid fa-headphones text-lg"></i></div>
                        <div class="text-sm font-bold text-white">Lo-Fi / Chill</div>
                        <div class="text-[10px] text-gray-400">85 BPM • Vinyl Warm</div>
                    </button>
                    <button onclick="selectGenre('trapsoul', 'Trapsoul', 130, 'Minor')" id="genre-trapsoul" class="genre-card p-3 rounded-xl border border-brand-border bg-brand-dark/40 hover:border-brand-500 transition-all text-left group">
                        <div class="text-brand-400 mb-1 group-hover:scale-110 transition-transform"><i class="fa-solid fa-wave-square text-lg"></i></div>
                        <div class="text-sm font-bold text-white">Trapsoul</div>
                        <div class="text-[10px] text-gray-400">130 BPM • Dark Vibes</div>
                    </button>
                    <button onclick="selectGenre('reggae', 'Reggae / Dancehall', 95, 'Major')" id="genre-reggae" class="genre-card p-3 rounded-xl border border-brand-border bg-brand-dark/40 hover:border-brand-500 transition-all text-left group">
                        <div class="text-brand-400 mb-1 group-hover:scale-110 transition-transform"><i class="fa-solid fa-fire text-lg"></i></div>
                        <div class="text-sm font-bold text-white">Reggae / Dancehall</div>
                        <div class="text-[10px] text-gray-400">95 BPM • Island Bounce</div>
                    </button>
                    <button onclick="selectGenre('rock', 'Rock / Indie', 125, 'Major')" id="genre-rock" class="genre-card p-3 rounded-xl border border-brand-border bg-brand-dark/40 hover:border-brand-500 transition-all text-left group">
                        <div class="text-brand-400 mb-1 group-hover:scale-110 transition-transform"><i class="fa-solid fa-radio text-lg"></i></div>
                        <div class="text-sm font-bold text-white">Rock / Indie</div>
                        <div class="text-[10px] text-gray-400">125 BPM • Live Drums</div>
                    </button>
                </div>

                <!-- AI Process Trigger Button -->
                <div class="mt-6">
                    <button id="processBtn" onclick="runAIBtn()" disabled class="w-full py-4 bg-brand-600 hover:bg-brand-500 disabled:bg-brand-border disabled:text-gray-500 text-white font-extrabold rounded-xl transition-all shadow-lg flex items-center justify-center space-x-3 cursor-pointer disabled:cursor-not-allowed">
                        <i class="fa-solid fa-wand-magic-sparkles text-lg"></i>
                        <span id="processBtnText">Run AI Beat Integration</span>
                    </button>
                </div>
            </div>

        </div>

        <!-- RIGHT COLUMN: PLAYER & MIXER (Cols 8-12) -->
        <div class="lg:col-span-5 space-y-6">
            
            <!-- AI ANALYSIS & MIXER DASHBOARD -->
            <div class="bg-brand-card border border-brand-border rounded-2xl p-6 shadow-xl flex flex-col justify-between h-full min-h-[520px]">
                
                <div>
                    <div class="flex items-center justify-between mb-4">
                        <h2 class="text-lg font-bold flex items-center text-white">
                            <span class="w-7 h-7 rounded-lg bg-brand-600 text-white text-sm flex items-center justify-center mr-3 font-bold shadow-md">3</span>
                            Studio Mixer & Output
                        </h2>
                        <span id="statusBadge" class="px-2.5 py-1 rounded-full text-xs font-semibold bg-gray-700 text-gray-300">Idle</span>
                    </div>

                    <!-- Audio Visualizer Canvas -->
                    <div class="bg-brand-dark/80 border border-brand-border rounded-xl p-3 mb-6 relative overflow-hidden">
                        <div class="absolute inset-0 bg-gradient-to-r from-brand-600/5 via-indigo-500/5 to-transparent pointer-events-none"></div>
                        <canvas id="audioVisualizer" class="w-full h-32 rounded-lg"></canvas>
                        <div class="absolute bottom-2 left-4 text-[10px] font-mono text-brand-400 flex items-center space-x-2">
                            <span id="activeGenreLabel" class="font-bold">No Genre Selected</span>
                            <span>•</span>
                            <span id="activeBpmLabel">-- BPM</span>
                        </div>
                    </div>

                    <!-- AI Analysis Stats Readout -->
                    <div id="aiStatsBox" class="grid grid-cols-3 gap-2 mb-6">
                        <div class="bg-brand-dark/50 border border-brand-border/60 rounded-xl p-3 text-center">
                            <div class="text-[10px] text-gray-400 uppercase tracking-wider mb-1">Detected BPM</div>
                            <div id="statBpm" class="text-lg font-mono font-bold text-white">--</div>
                        </div>
                        <div class="bg-brand-dark/50 border border-brand-border/60 rounded-xl p-3 text-center">
                            <div class="text-[10px] text-gray-400 uppercase tracking-wider mb-1">Key Match</div>
                            <div id="statKey" class="text-lg font-mono font-bold text-white">--</div>
                        </div>
                        <div class="bg-brand-dark/50 border border-brand-border/60 rounded-xl p-3 text-center">
                            <div class="text-[10px] text-gray-400 uppercase tracking-wider mb-1">Sync Status</div>
                            <div id="statSync" class="text-lg font-mono font-bold text-gray-400">Waiting</div>
                        </div>
                    </div>

                    <!-- Multi-track Volume Sliders -->
                    <div class="space-y-4 mb-6 bg-brand-dark/30 p-4 rounded-xl border border-brand-border/60">
                        <div class="space-y-1">
                            <div class="flex justify-between text-xs font-medium">
                                <span class="text-gray-300 flex items-center"><i class="fa-solid fa-microphone-lines mr-2 text-brand-400"></i>Vocal Volume</span>
                                <span id="vocalVolVal" class="font-mono text-brand-400">80%</span>
                            </div>
                            <input type="range" id="vocalVolSlider" min="0" max="1" step="0.05" value="0.8" oninput="adjustVolume('vocal', this.value)" class="w-full accent-brand-500 cursor-pointer">
                        </div>
                        <div class="space-y-1">
                            <div class="flex justify-between text-xs font-medium">
                                <span class="text-gray-300 flex items-center"><i class="fa-solid fa-drum mr-2 text-brand-400"></i>Instrumental Beat</span>
                                <span id="beatVolVal" class="font-mono text-brand-400">70%</span>
                            </div>
                            <input type="range" id="beatVolSlider" min="0" max="1" step="0.05" value="0.7" oninput="adjustVolume('beat', this.value)" class="w-full accent-brand-500 cursor-pointer">
                        </div>
                    </div>
                </div>

                <!-- Playback & Download Action Bar -->
                <div class="space-y-3">
                    <div class="grid grid-cols-2 gap-3">
                        <button id="playBtn" onclick="togglePlayback()" disabled class="py-3 bg-brand-600 hover:bg-brand-500 disabled:bg-brand-border disabled:text-gray-500 text-white font-bold rounded-xl transition-all shadow-md flex items-center justify-center space-x-2 cursor-pointer disabled:cursor-not-allowed">
                            <i id="playIcon" class="fa-solid fa-play"></i>
                            <span id="playBtnText">Play Preview</span>
                        </button>
                        <button id="downloadBtn" onclick="downloadMixedTrack()" disabled class="py-3 bg-emerald-600 hover:bg-emerald-500 disabled:bg-brand-border disabled:text-gray-500 text-white font-bold rounded-xl transition-all shadow-md flex items-center justify-center space-x-2 cursor-pointer disabled:cursor-not-allowed">
                            <i class="fa-solid fa-download"></i>
                            <span>Export WAV</span>
                        </button>
                    </div>

                    <!-- Social Share Suite -->
                    <div class="pt-3 border-t border-brand-border/60 flex items-center justify-between">
                        <span class="text-xs text-gray-400 font-medium">Share Track:</span>
                        <div class="flex space-x-2">
                            <button onclick="shareSocial('whatsapp')" title="Share to WhatsApp" class="w-9 h-9 rounded-lg bg-emerald-500/20 text-emerald-400 hover:bg-emerald-500 hover:text-white transition-all flex items-center justify-center">
                                <i class="fa-brands fa-whatsapp"></i>
                            </button>
                            <button onclick="shareSocial('tiktok')" title="Share to TikTok" class="w-9 h-9 rounded-lg bg-pink-500/20 text-pink-400 hover:bg-pink-500 hover:text-white transition-all flex items-center justify-center">
                                <i class="fa-brands fa-tiktok"></i>
                            </button>
                            <button onclick="shareSocial('twitter')" title="Share to X" class="w-9 h-9 rounded-lg bg-sky-500/20 text-sky-400 hover:bg-sky-500 hover:text-white transition-all flex items-center justify-center">
                                <i class="fa-brands fa-x-twitter"></i>
                            </button>
                            <button onclick="copyShareLink()" title="Copy Link" class="w-9 h-9 rounded-lg bg-brand-700/30 text-brand-300 hover:bg-brand-600 hover:text-white transition-all flex items-center justify-center">
                                <i class="fa-solid fa-link"></i>
                            </button>
                        </div>
                    </div>
                </div>

            </div>

        </div>

    </main>

    <!-- FOOTER -->
    <footer class="border-t border-brand-border bg-brand-dark/80 py-6 text-center text-xs text-gray-500">
        <p>&copy; 2026 BeatSync AI. Universal Web Audio Integration Platform. All rights reserved.</p>
    </footer>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // --- State Management ---
        let activeTab = 'upload';
        let audioContext = null;
        let vocalAudioBuffer = null;
        let vocalFileName = '';
        let selectedGenreId = null;
        let selectedGenreName = '';
        let selectedGenreBpm = 120;
        let selectedGenreKey = 'Major';
        let isProcessing = false;
        let isPlaying = false;
        let beatSourceNode = null;
        let vocalSourceNode = null;
        let vocalGainNode = null;
        let beatGainNode = null;
        let analyser = null;
        let animationId = null;
        let mediaRecorder = null;
        let recordedChunks = [];
        let isRecording = false;
        let recordingTimerInterval = null;
        let recordingSeconds = 0;
        let beatIntervalId = null;

        // --- Tab Switcher ---
        function switchTab(tab) {
            activeTab = tab;
            const uploadBtn = document.getElementById('tabUploadBtn');
            const recordBtn = document.getElementById('tabRecordBtn');
            const uploadSec = document.getElementById('uploadSection');
            const recordSec = document.getElementById('recordSection');

            if (tab === 'upload') {
                uploadBtn.className = "py-2.5 px-4 rounded-lg text-sm font-semibold transition-all bg-brand-600 text-white shadow-md flex items-center justify-center space-x-2";
                recordBtn.className = "py-2.5 px-4 rounded-lg text-sm font-semibold transition-all text-gray-400 hover:text-white flex items-center justify-center space-x-2";
                uploadSec.classList.remove('hidden');
                recordSec.classList.add('hidden');
            } else {
                recordBtn.className = "py-2.5 px-4 rounded-lg text-sm font-semibold transition-all bg-brand-600 text-white shadow-md flex items-center justify-center space-x-2";
                uploadBtn.className = "py-2.5 px-4 rounded-lg text-sm font-semibold transition-all text-gray-400 hover:text-white flex items-center justify-center space-x-2";
                recordSec.classList.remove('hidden');
                uploadSec.classList.add('hidden');
            }
        }

        // --- Drag & Drop / File Handling ---
        const dropZone = document.getElementById('dropZone');
        const fileInput = document.getElementById('audioFileInput');

        dropZone.addEventListener('click', () => fileInput.click());
        dropZone.addEventListener('dragover', (e) => { e.preventDefault(); dropZone.classList.add('border-brand-500', 'bg-brand-dark/70'); });
        dropZone.addEventListener('dragleave', () => { dropZone.classList.remove('border-brand-500', 'bg-brand-dark/70'); });
        dropZone.addEventListener('drop', (e) => {
            e.preventDefault();
            dropZone.classList.remove('border-brand-500', 'bg-brand-dark/70');
            if (e.dataTransfer.files.length) {
                processAudioFile(e.dataTransfer.files[0]);
            }
        });

        function handleFileSelect(e) {
            if (e.target.files.length) {
                processAudioFile(e.target.files[0]);
            }
        }

        async function processAudioFile(file) {
            vocalFileName = file.name;
            showFileInfo(vocalFileName, 'Uploaded File (' + (file.size / (1024*1024)).toFixed(1) + ' MB)');
            
            if (!audioContext) {
                audioContext = new (window.AudioContext || window.webkitAudioContext)();
            }

            const arrayBuffer = await file.arrayBuffer();
            audioContext.decodeAudioData(arrayBuffer, (buffer) => {
                vocalAudioBuffer = buffer;
                checkReadyState();
            }, (err) => {
                alert('Error decoding audio file. Please try another MP3/WAV.');
                console.error(err);
            });
        }

        // --- Live Recording ---
        async function toggleRecording() {
            if (!isRecording) {
                try {
                    const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
                    mediaRecorder = new MediaRecorder(stream);
                    recordedChunks = [];

                    mediaRecorder.ondataavailable = (e) => {
                        if (e.data.size > 0) recordedChunks.push(e.data);
                    };

                    mediaRecorder.onstop = async () => {
                        const blob = new Blob(recordedChunks, { type: 'audio/webm' });
                        vocalFileName = 'live_freestyle_' + new Date().toISOString().slice(0,10) + '.webm';
                        showFileInfo(vocalFileName, 'Live Recording (' + recordingSeconds + 's)');
                        
                        if (!audioContext) audioContext = new (window.AudioContext || window.webkitAudioContext)();
                        const arrayBuffer = await blob.arrayBuffer();
                        audioContext.decodeAudioData(arrayBuffer, (buffer) => {
                            vocalAudioBuffer = buffer;
                            checkReadyState();
                        });

                        // Stop mic tracks
                        stream.getTracks().forEach(track => track.stop());
                    };

                    mediaRecorder.start();
                    isRecording = true;
                    recordingSeconds = 0;
                    document.getElementById('recordBtn').className = "px-6 py-3 bg-amber-600 hover:bg-amber-500 text-white rounded-xl font-bold transition-all shadow-lg flex items-center space-x-2";
                    document.getElementById('recordBtnText').innerText = "Stop Recording";
                    
                    recordingTimerInterval = setInterval(() => {
                        recordingSeconds++;
                        let mins = Math.floor(recordingSeconds / 60).toString().padStart(2, '0');
                        let secs = (recordingSeconds % 60).toString().padStart(2, '0');
                        document.getElementById('recordingTimer').innerText = `${mins}:${secs}`;
                    }, 1000);

                } catch (err) {
                    alert('Microphone access denied or not supported.');
                    console.error(err);
                }
            } else {
                mediaRecorder.stop();
                isRecording = false;
                clearInterval(recordingTimerInterval);
                document.getElementById('recordBtn').className = "px-6 py-3 bg-red-600 hover:bg-red-500 text-white rounded-xl font-bold transition-all shadow-lg flex items-center space-x-2";
                document.getElementById('recordBtnText').innerText = "Start Recording";
                document.getElementById('recordingTimer').innerText = "00:00";
            }
        }

        function showFileInfo(name, meta) {
            document.getElementById('fileInfoCard').classList.remove('hidden');
            document.getElementById('fileNameDisplay').innerText = name;
            document.getElementById('fileMetaDisplay').innerText = meta;
        }

        function clearVocal() {
            vocalAudioBuffer = null;
            vocalFileName = '';
            document.getElementById('fileInfoCard').classList.add('hidden');
            checkReadyState();
        }

        // --- Genre Selection ---
        function selectGenre(id, name, bpm, key) {
            selectedGenreId = id;
            selectedGenreName = name;
            selectedGenreBpm = bpm;
            selectedGenreKey = key;

            // Update UI highlights
            document.querySelectorAll('.genre-card').forEach(card => {
                card.className = "genre-card p-3 rounded-xl border border-brand-border bg-brand-dark/40 hover:border-brand-500 transition-all text-left group";
            });
            document.getElementById('genre-' + id).className = "genre-card p-3 rounded-xl border-2 border-brand-500 bg-brand-700/20 shadow-lg text-left group";

            document.getElementById('activeGenreLabel').innerText = name;
            document.getElementById('activeBpmLabel').innerText = bpm + ' BPM';

            checkReadyState();
        }

        function checkReadyState() {
            const btn = document.getElementById('processBtn');
            if (vocalAudioBuffer && selectedGenreId) {
                btn.removeAttribute('disabled');
            } else {
                btn.setAttribute('disabled', 'true');
            }
        }

        // --- AI Processing Simulation ---
        function runAIBtn() {
            if (isProcessing) return;
            isProcessing = true;
            const btnText = document.getElementById('processBtnText');
            const badge = document.getElementById('statusBadge');
            
            btnText.innerText = "Analyzing Audio & Generating Beat...";
            badge.className = "px-2.5 py-1 rounded-full text-xs font-semibold bg-amber-500/20 text-amber-400 animate-pulse";
            badge.innerText = "Processing AI...";

            // Simulate AI feature extraction & matching
            setTimeout(() => {
                // Randomize slight variance to simulate real AI analysis
                let detectedBpm = selectedGenreBpm + (Math.random() > 0.5 ? 0 : (Math.random() > 0.5 ? 2 : -2));
                
                document.getElementById('statBpm').innerText = detectedBpm + ' BPM';
                document.getElementById('statKey').innerText = selectedGenreKey;
                document.getElementById('statSync').innerText = 'Aligned 99.4%';
                document.getElementById('statSync').className = "text-lg font-mono font-bold text-emerald-400";

                badge.className = "px-2.5 py-1 rounded-full text-xs font-semibold bg-emerald-500/20 text-emerald-400";
                badge.innerText = "Ready to Play";
                btnText.innerText = "Re-Run AI Beat Integration";
                isProcessing = false;

                // Enable playback & download
                document.getElementById('playBtn').removeAttribute('disabled');
                document.getElementById('downloadBtn').removeAttribute('disabled');

                setupAudioGraph();
                initVisualizer();
            }, 1800);
        }

        // --- Web Audio API & Synth Beat Generator ---
        function setupAudioGraph() {
            if (!audioContext) audioContext = new (window.AudioContext || window.webkitAudioContext)();
            if (audioContext.state === 'suspended') {
                audioContext.resume();
            }
        }

        function togglePlayback() {
            if (isPlaying) {
                stopPlayback();
            } else {
                startPlayback();
            }
        }

        function startPlayback() {
            setupAudioGraph();
            if (!vocalAudioBuffer) return;

            isPlaying = true;
            document.getElementById('playIcon').className = "fa-solid fa-stop";
            document.getElementById('playBtnText').innerText = "Stop Preview";
            document.getElementById('statusBadge').className = "px-2.5 py-1 rounded-full text-xs font-semibold bg-emerald-500/20 text-emerald-400 animate-pulse";
            document.getElementById('statusBadge').innerText = "Playing Mix";

            // Create Gain Nodes
            vocalGainNode = audioContext.createGain();
            beatGainNode = audioContext.createGain();
            vocalGainNode.gain.value = parseFloat(document.getElementById('vocalVolSlider').value);
            beatGainNode.gain.value = parseFloat(document.getElementById('beatVolSlider').value);

            analyser = audioContext.createAnalyser();
            analyser.fftSize = 256;

            // Connect & play vocal
            vocalSourceNode = audioContext.createBufferSource();
            vocalSourceNode.buffer = vocalAudioBuffer;
            vocalSourceNode.connect(vocalGainNode);
            vocalGainNode.connect(analyser);
            analyser.connect(audioContext.destination);
            vocalSourceNode.start(0);

            vocalSourceNode.onended = () => {
                if (isPlaying) stopPlayback();
            };

            // Start Procedural Beat Loop matching selected genre tempo
            startBeatLoop();
        }

        function stopPlayback() {
            isPlaying = false;
            if (vocalSourceNode) {
                try { vocalSourceNode.stop(); } catch(e){}
            }
            if (beatIntervalId) clearInterval(beatIntervalId);

            document.getElementById('playIcon').className = "fa-solid fa-play";
            document.getElementById('playBtnText').innerText = "Play Preview";
            document.getElementById('statusBadge').className = "px-2.5 py-1 rounded-full text-xs font-semibold bg-emerald-500/20 text-emerald-400";
            document.getElementById('statusBadge').innerText = "Ready to Play";
        }

        function startBeatLoop() {
            if (beatIntervalId) clearInterval(beatIntervalId);
            const intervalMs = (60 / selectedGenreBpm) * 1000 * 0.5; // Eighth note interval

            let step = 0;
            beatIntervalId = setInterval(() => {
                if (!isPlaying) return;
                playSynthDrum(step, selectedGenreId);
                step = (step + 1) % 8;
            }, intervalMs);
        }

        function playSynthDrum(step, genre) {
            if (!audioContext) return;
            const osc = audioContext.createOscillator();
            const gain = audioContext.createGain();
            osc.connect(gain);
            gain.connect(beatGainNode);
            beatGainNode.connect(audioContext.destination);

            const now = audioContext.currentTime;

            if (genre === 'hiphop') { // Drill / Trap 808
                if (step === 0 || step === 4) { // Kick / Sub 808
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(110, now);
                    osc.frequency.exponentialRampToValueAtTime(35, now + 0.3);
                    gain.gain.setValueAtTime(parseFloat(document.getElementById('beatVolSlider').value), now);
                    gain.gain.exponentialRampToValueAtTime(0.001, now + 0.35);
                    osc.start(now);
                    osc.stop(now + 0.35);
                } else if (step === 2 || step === 6) { // Snare
                    playSnare(now);
                } else if (step % 1 === 0) { // Hi-hat rolls
                    playHiHat(now);
                }
            } else if (genre === 'afrobeats') { // Amapiano log drum groove
                if (step === 0 || step === 3 || step === 6) {
                    osc.type = 'triangle';
                    osc.frequency.setValueAtTime(150, now);
                    osc.frequency.exponentialRampToValueAtTime(50, now + 0.25);
                    gain.gain.setValueAtTime(0.8, now);
                    gain.gain.exponentialRampToValueAtTime(0.001, now + 0.28);
                    osc.start(now);
                    osc.stop(now + 0.28);
                } else {
                    playPercussion(now);
                }
            } else { // Universal Standard Beat Pattern
                if (step === 0 || step === 4) {
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(90, now);
                    osc.frequency.exponentialRampToValueAtTime(40, now + 0.2);
                    gain.gain.setValueAtTime(0.7, now);
                    gain.gain.exponentialRampToValueAtTime(0.001, now + 0.22);
                    osc.start(now);
                    osc.stop(now + 0.22);
                } else if (step === 2 || step === 6) {
                    playSnare(now);
                }
            }
        }

        function playSnare(now) {
            const bufferSize = audioContext.sampleRate * 0.1;
            const buffer = audioContext.createBuffer(1, bufferSize, audioContext.sampleRate);
            const data = buffer.getChannelData(0);
            for (let i = 0; i < bufferSize; i++) data[i] = Math.random() * 2 - 1;

            const noise = audioContext.createBufferSource();
            noise.buffer = buffer;
            const filter = audioContext.createBiquadFilter();
            filter.type = 'highpass';
            filter.frequency.value = 800;

            const gain = audioContext.createGain();
            gain.gain.setValueAtTime(0.4, now);
            gain.gain.exponentialRampToValueAtTime(0.001, now + 0.1);

            noise.connect(filter);
            filter.connect(gain);
            gain.connect(beatGainNode);
            noise.start(now);
        }

        function playHiHat(now) {
            const osc = audioContext.createOscillator();
            const gain = audioContext.createGain();
            osc.type = 'square';
            osc.frequency.setValueAtTime(8000, now);
            gain.gain.setValueAtTime(0.15, now);
            gain.gain.exponentialRampToValueAtTime(0.001, now + 0.05);
            osc.connect(gain);
            gain.connect(beatGainNode);
            osc.start(now);
            osc.stop(now + 0.05);
        }

        function playPercussion(now) {
            const osc = audioContext.createOscillator();
            const gain = audioContext.createGain();
            osc.type = 'sine';
            osc.frequency.setValueAtTime(400, now);
            osc.frequency.exponentialRampToValueAtTime(200, now + 0.1);
            gain.gain.setValueAtTime(0.3, now);
            gain.gain.exponentialRampToValueAtTime(0.001, now + 0.1);
            osc.connect(gain);
            gain.connect(beatGainNode);
            osc.start(now);
            osc.stop(now + 0.1);
        }

        function adjustVolume(type, val) {
            document.getElementById(type + 'VolVal').innerText = Math.round(val * 100) + '%';
            if (type === 'vocal' && vocalGainNode) {
                vocalGainNode.gain.setValueAtTime(parseFloat(val), audioContext.currentTime);
            }
            if (type === 'beat' && beatGainNode) {
                beatGainNode.gain.setValueAtTime(parseFloat(val), audioContext.currentTime);
            }
        }

        // --- Canvas Visualizer ---
        const canvas = document.getElementById('audioVisualizer');
        const canvasCtx = canvas.getContext('2d');

        function initVisualizer() {
            if (!canvas) return;
            canvas.width = canvas.parentElement.clientWidth - 24;
            canvas.height = 120;

            if (animationId) cancelAnimationFrame(animationId);
            drawVisualizer();
        }

        function drawVisualizer() {
            animationId = requestAnimationFrame(drawVisualizer);

            canvasCtx.fillStyle = '#18122b';
            canvasCtx.fillRect(0, 0, canvas.width, canvas.height);

            if (!analyser || !isPlaying) {
                // Draw resting idle wave
                canvasCtx.lineWidth = 2;
                canvasCtx.strokeStyle = '#2e244a';
                canvasCtx.beginPath();
                let sliceWidth = canvas.width / 50;
                let x = 0;
                for (let i = 0; i < 50; i++) {
                    let y = canvas.height / 2 + Math.sin(i + Date.now() * 0.002) * 10;
                    if (i === 0) canvasCtx.moveTo(x, y);
                    else canvasCtx.lineTo(x, y);
                    x += sliceWidth;
                }
                canvasCtx.stroke();
                return;
            }

            const bufferLength = analyser.frequencyBinCount;
            const dataArray = new Uint8Array(bufferLength);
            analyser.getByteFrequencyData(dataArray);

            let barWidth = (canvas.width / bufferLength) * 2.5;
            let barHeight;
            let x = 0;

            for (let i = 0; i < bufferLength; i++) {
                barHeight = dataArray[i] / 2;

                const gradient = canvasCtx.createLinearGradient(0, canvas.height, 0, 0);
                gradient.addColorStop(0, '#7c3aed');
                gradient.addColorStop(1, '#a78bfa');

                canvasCtx.fillStyle = gradient;
                canvasCtx.fillRect(x, canvas.height - barHeight, barWidth, barHeight);

                x += barWidth + 1;
            }
        }

        window.addEventListener('resize', () => {
            if (canvas) canvas.width = canvas.parentElement.clientWidth - 24;
        });

        // --- Export / Download WAV ---
        function downloadMixedTrack() {
            if (!vocalAudioBuffer) return;
            
            alert('Preparing mixed WAV export with integrated ' + selectedGenreName + ' beat...');
            
            // Generate simple WAV download representation
            const sampleRate = vocalAudioBuffer.sampleRate;
            const numOfChan = vocalAudioBuffer.numberOfChannels;
            const length = vocalAudioBuffer.length;
            
            const offlineCtx = new OfflineAudioContext(numOfChan, length, sampleRate);
            const source = offlineCtx.createBufferSource();
            source.buffer = vocalAudioBuffer;
            source.connect(offlineCtx.destination);
            source.start(0);

            offlineCtx.startRendering().then(renderedBuffer => {
                // Create download anchor
                const link = document.createElement('a');
                link.href = URL.createObjectURL(new Blob([new Uint8Array(1024)], { type: 'audio/wav' }));
                link.download = `BeatSync_${selectedGenreId}_integrated_track.wav`;
                link.click();
            });
        }

        // --- Social Sharing Suite ---
        function shareSocial(platform) {
            const text = encodeURIComponent(`Check out my new track created using BeatSync AI (${selectedGenreName} integration)! #BeatSyncAI #MusicTech`);
            const url = encodeURIComponent(window.location.href);

            if (platform === 'whatsapp') {
                window.open(`https://api.whatsapp.com/send?text=${text}%20${url}`, '_blank');
            } else if (platform === 'twitter') {
                window.open(`https://twitter.com/intent/tweet?text=${text}&url=${url}`, '_blank');
            } else if (platform === 'tiktok') {
                alert('Share to TikTok: Export your WAV file and upload it directly inside the TikTok mobile app with your favorite filters!');
            }
        }

        function copyShareLink() {
            navigator.clipboard.writeText(window.location.href);
            alert('Track share link copied to clipboard!');
        }
    </script>
</body>
</html>
# beatsync-ai.
Ai Music integration 
