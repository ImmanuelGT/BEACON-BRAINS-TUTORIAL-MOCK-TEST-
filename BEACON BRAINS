<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BEACON BRAINS | Professional Examination Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
        
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            user-select: none;
            -webkit-user-select: none;
            background-color: #020617;
            color: #f8fafc;
            overflow-x: hidden;
        }

        .glass-card {
            background: rgba(15, 23, 42, 0.8);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
        }

        .btn-primary {
            background: linear-gradient(135deg, #6366f1 0%, #4338ca 100%);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px -5px rgba(99, 102, 241, 0.4);
        }

        .palette-btn.answered { background-color: #10b981 !important; border-color: #059669 !important; color: white !important; }
        .palette-btn.flagged { background-color: #f59e0b !important; border-color: #d97706 !important; color: white !important; }
        .palette-btn.current { outline: 2px solid #6366f1 !important; outline-offset: 2px; background-color: #1e1b4b !important; }

        .modal-overlay {
            background: rgba(2, 6, 23, 0.95);
            backdrop-filter: blur(8px);
        }

        .instruction-item {
            border-left: 3px solid #6366f1;
            padding-left: 1rem;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #334155; border-radius: 10px; }
    </style>
</head>
<body class="min-h-screen">

    <!-- Confirmation Modal -->
    <div id="submit-modal" class="fixed inset-0 z-[110] hidden modal-overlay flex items-center justify-center p-4">
        <div class="glass-card p-8 rounded-3xl max-w-md w-full border border-slate-700 text-center">
            <div class="w-16 h-16 bg-indigo-500/20 text-indigo-400 rounded-full flex items-center justify-center mx-auto mb-6">
                <i class="fas fa-paper-plane text-2xl"></i>
            </div>
            <h3 class="text-2xl font-bold mb-2">Final Submission</h3>
            <p class="text-slate-400 mb-6" id="unanswered-count"></p>
            <div class="flex gap-4">
                <button onclick="closeSubmitModal()" class="flex-1 px-6 py-3 rounded-xl bg-slate-800 hover:bg-slate-700 font-bold">Review</button>
                <button onclick="confirmSubmission()" class="flex-1 px-6 py-3 rounded-xl btn-primary font-bold">Submit Now</button>
            </div>
        </div>
    </div>

    <!-- Anti-Cheat Overlay -->
    <div id="cheat-warning" class="fixed inset-0 z-[120] hidden modal-overlay flex items-center justify-center p-4">
        <div class="bg-slate-900 border-2 border-red-500 p-8 rounded-3xl max-w-md text-center shadow-2xl">
            <i class="fas fa-shield-halved text-red-500 text-5xl mb-4"></i>
            <h2 class="text-2xl font-bold mb-2">SECURITY VIOLATION</h2>
            <p class="text-slate-400 mb-6 text-sm">Window focus lost. This event has been logged for administrative review. Please remain in the browser window to avoid automatic disqualification.</p>
            <button onclick="dismissCheatWarning()" class="w-full btn-primary py-3 rounded-xl font-bold">RESUME EXAM</button>
        </div>
    </div>

    <div id="app" class="container mx-auto px-4 py-8 max-w-6xl"></div>

    <button id="calc-toggle" onclick="toggleCalculator()" class="fixed bottom-6 right-6 w-14 h-14 bg-indigo-600 rounded-full shadow-2xl flex items-center justify-center text-white z-50 hover:bg-indigo-500 hidden transition-all">
        <i class="fas fa-calculator"></i>
    </button>

    <div id="calc-modal" class="fixed bottom-24 right-6 w-72 glass-card rounded-2xl p-4 shadow-2xl z-50 hidden">
        <div class="flex justify-between items-center mb-3">
            <span class="text-[10px] font-bold text-slate-500 uppercase tracking-widest">Scientific Utils</span>
            <button onclick="toggleCalculator()" class="text-slate-500 hover:text-white"><i class="fas fa-times"></i></button>
        </div>
        <input type="text" id="calc-display" readonly class="w-full bg-black/40 border border-slate-800 rounded-lg p-3 text-right text-xl font-mono mb-3 text-indigo-400" value="0">
        <div class="grid grid-cols-4 gap-2">
            <button onclick="calcClear()" class="p-2 bg-red-500/10 text-red-400 rounded hover:bg-red-500/20">C</button>
            <button onclick="calcOp('sqrt')" class="p-2 bg-slate-800 rounded">√</button>
            <button onclick="calcOp('%')" class="p-2 bg-slate-800 rounded">%</button>
            <button onclick="calcOp('/')" class="p-2 bg-indigo-500/10 text-indigo-400 rounded">÷</button>
            <button onclick="calcNum('7')" class="p-2 bg-slate-800 rounded">7</button>
            <button onclick="calcNum('8')" class="p-2 bg-slate-800 rounded">8</button>
            <button onclick="calcNum('9')" class="p-2 bg-slate-800 rounded">9</button>
            <button onclick="calcOp('*')" class="p-2 bg-indigo-500/10 text-indigo-400 rounded">×</button>
            <button onclick="calcNum('4')" class="p-2 bg-slate-800 rounded">4</button>
            <button onclick="calcNum('5')" class="p-2 bg-slate-800 rounded">5</button>
            <button onclick="calcNum('6')" class="p-2 bg-slate-800 rounded">6</button>
            <button onclick="calcOp('-')" class="p-2 bg-indigo-500/10 text-indigo-400 rounded">-</button>
            <button onclick="calcNum('1')" class="p-2 bg-slate-800 rounded">1</button>
            <button onclick="calcNum('2')" class="p-2 bg-slate-800 rounded">2</button>
            <button onclick="calcNum('3')" class="p-2 bg-slate-800 rounded">3</button>
            <button onclick="calcOp('+')" class="p-2 bg-indigo-500/10 text-indigo-400 rounded">+</button>
            <button onclick="calcNum('0')" class="p-2 bg-slate-800 rounded col-span-2">0</button>
            <button onclick="calcNum('.')" class="p-2 bg-slate-800 rounded">.</button>
            <button onclick="calcEqual()" class="p-2 bg-indigo-600 text-white rounded">=</button>
        </div>
    </div>

    <script>
        const QUESTIONS = [
            { q: "Which of the following blood vessels carries oxygenated blood away from the heart?", options: ["Venules", "Veins", "Arteries", "Capillaries"], correct: 2, explain: "Arteries carry oxygenated blood away from the heart to the rest of the body, with the exception of the pulmonary artery." },
            { q: "Which of the following statements is true regarding sexual reproduction in organisms?", options: ["Asexual variant", "No gametes", "Identical offspring", "Fusion of gametes from two parents"], correct: 3, explain: "Sexual reproduction involves the fusion of haploid male and female gametes to form a diploid zygote, resulting in genetic variation." },
            { q: "Which of the following statements best describes the role of competition in adaptation?", options: ["Equal distribution", "Reduces need for adaptation", "Develops new traits", "Selection of individuals with favorable traits"], correct: 3, explain: "Competition for limited resources leads to natural selection, where individuals with traits best suited to their environment are more likely to survive and reproduce." },
            { q: "Digestive enzymes are responsible for", options: ["Breaking down food into smaller molecules", "Absorbing nutrients", "Regulating pH", "Transporting food"], correct: 0, explain: "Enzymes act as biological catalysts that break down complex macromolecules (like starch and proteins) into simple, absorbable units." },
            { q: "Which statement is true about the kingdom Fungi?", options: ["Photosynthetic", "Absorb organic matter", "Always multicellular", "Produce seeds"], correct: 1, explain: "Fungi are heterotrophic organisms that obtain nutrients by absorbing dissolved organic matter through their cell walls (saprophytic or parasitic)." },
            { q: "Ecological succession refers to", options: ["Movement of organisms", "Gradual change in community over time", "Competition for resources", "Natural selection"], correct: 1, explain: "Succession is the predictable process by which the structure of a biological community evolves over time." },
            { q: "Which is the most inclusive level of classification in the Linnaean system?", options: ["Kingdom", "Order", "Class", "Phylum"], correct: 0, explain: "In the taxonomic hierarchy, Kingdom is the highest and most inclusive level among the options provided." },
            { q: "Trophic levels in an ecosystem describe", options: ["Nutrient cycling", "Biodiversity", "Ecological interaction", "Levels of energy flow"], correct: 3, explain: "Trophic levels represent the feeding positions in a food chain or web, indicating how energy flows from producers to various consumers." },
            { q: "The primary function of the urinary tubule is", options: ["Production of urine", "Connecting kidneys to bladder", "Regulating electrolyte balance", "Filtration of blood"], correct: 0, explain: "The urinary tubules (nephrons) are the functional units of the kidney responsible for the concentration and production of urine." },
            { q: "Courtship behaviors in animals", options: ["Aggressive interactions", "Displays to attract a mate", "Female only displays", "Dominance establishment"], correct: 1, explain: "Courtship involves specific behaviors or signals used to attract mates and ensure successful reproduction within the same species." },
            { q: "Structure in the ear transmitting vibrations to the auditory nerve?", options: ["Auditory canal", "Cochlea", "Eardrum", "Ossicles"], correct: 1, explain: "The cochlea contains hair cells that convert mechanical vibrations into electrical impulses for the auditory nerve." },
            { q: "Plant hormone responsible for cell elongation?", options: ["Gibberellins", "Abscisic acid", "Ethylene", "Cytokinins"], correct: 0, explain: "Gibberellins are primarily responsible for stimulating cell elongation and stem growth." },
            { q: "Correct hierarchy from smallest to largest:", options: ["Organs to Cells", "Cells to Ecosystems", "Tissues to Communities", "Atoms to Organs"], correct: 1, explain: "Biological organization flows from Cells → Tissues → Organs → Organ Systems → Organism → Population → Community → Ecosystem." },
            { q: "Metamorphosis involves", options: ["Change in form during life cycle", "Adult to larval change", "Zygote growth", "Regeneration"], correct: 0, explain: "Metamorphosis is a biological process by which an animal physically develops after birth or hatching, involving a conspicuous change in form." },
            { q: "A natural habitat is", options: ["Where organisms naturally live", "A lab setting", "Human-created wildlife park", "Protected area for endangered"], correct: 0, explain: "A habitat is the specific natural environment in which a particular species of organism lives and thrives." },
            { q: "Carbohydrates are classified as:", options: ["Micronutrient", "Phytonutrient", "Lipid", "Macronutrient"], correct: 3, explain: "Carbohydrates, along with proteins and fats, are macronutrients because they are required in large amounts for energy." },
            { q: "Cell growth occurs by", options: ["Organelle increase", "External factors only", "Cell division", "Continuous process"], correct: 2, explain: "Biological growth in multicellular organisms is primarily achieved through mitosis (cell division)." },
            { q: "Germination is when a seed", options: ["Absorbs soil nutrients", "Breaks dormancy to grow", "Begins photosynthesis", "Matures"], correct: 1, explain: "Germination is the process by which an organism grows from a seed or similar structure after a period of dormancy." },
            { q: "Physiological variation refers to", options: ["Genetic makeup differences", "Variations in functions and processes", "Physical appearance", "Social behavior"], correct: 1, explain: "Physiological variations are differences in the internal working of the body, such as blood group or metabolic rate." },
            { q: "Inability to focus light on the retina is known as", options: ["Cataracts", "Myopia", "Glaucoma", "Astigmatism"], correct: 1, explain: "Myopia (nearsightedness) occurs when light focuses in front of the retina rather than directly on it." },
            { q: "Adaptation is defined as", options: ["New traits from environment", "Changing environment", "Inherited trait for survival", "Acquired characteristics"], correct: 2, explain: "Adaptations are traits shaped by natural selection that improve an organism's fitness in its specific environment." },
            { q: "Excretory organs in humans include", options: ["Lungs, kidneys, and skin", "Heart, liver, spleen", "Brain, nerves", "Stomach, bladder"], correct: 0, explain: "Lungs excrete CO2, kidneys excrete urea/urine, and skin excretes salts and water through sweat." },
            { q: "Pollination is the transfer of pollen from", options: ["Anther to Stigma", "Stigma to Anther", "Stamen to Petal", "Root to Stem"], correct: 0, explain: "Pollination is the transfer of pollen from the male part (anther) to the female part (stigma) of a flower." },
            { q: "Method of asexual reproduction in plants?", options: ["Fertilization", "Vegetative propagation", "Pollination", "Dispersal"], correct: 1, explain: "Vegetative propagation allows plants to reproduce without seeds or spores, using stems, roots, or leaves." },
            { q: "Final electron acceptor in cellular respiration?", options: ["Glucose", "Oxygen", "Water", "CO2"], correct: 1, explain: "In aerobic respiration, oxygen is the final electron acceptor in the electron transport chain." },
            { q: "Primary function of the liver?", options: ["Blood pressure", "Temperature", "Detoxification", "Hormones"], correct: 2, explain: "The liver filters blood coming from the digestive tract and detoxifies chemicals and metabolizes drugs." },
            { q: "Tissue transporting water from roots?", options: ["Mesophyll", "Xylem", "Phloem", "Epidermis"], correct: 1, explain: "Xylem transports water and minerals upwards from roots, while phloem transports sugars from leaves." },
            { q: "Support in plants is provided by", options: ["Cell walls and turgor pressure", "Muscles", "Endocrine system", "Exoskeleton"], correct: 0, explain: "The rigid cell wall and internal water pressure (turgidity) provide structural support for plants." },
            { q: "Distinction of monocots from dicots?", options: ["Reproduction method", "Vascular bundles", "Number of cotyledons", "Root type"], correct: 2, explain: "Monocots have one seed leaf (cotyledon), while dicots have two." },
            { q: "Primary source of aquatic pollution?", options: ["Air pollution", "Deforestation", "Soil erosion", "Industrial discharge"], correct: 3, explain: "Industrial discharge often contains heavy metals and chemicals that directly contaminate water bodies." },
            { q: "Resource conservation example?", options: ["Sustainable fishing", "Excessive fertilizer", "Invasive species", "Deforestation"], correct: 0, explain: "Sustainable fishing ensures fish populations are maintained at healthy levels for the future." },
            { q: "Viviparity means offspring develop", options: ["Outside body", "External fertilization", "In eggs", "Inside the female"], correct: 3, explain: "Viviparous animals give birth to live young that have developed inside the mother's body." },
            { q: "Inheritance of traits is the study of", options: ["Selection", "Genetics", "Evolution", "Adaptation"], correct: 1, explain: "Genetics is the branch of biology concerned with the study of genes, genetic variation, and heredity." },
            { q: "Unique feature of plant cells?", options: ["Cell wall", "Chloroplasts", "Large central vacuole", "All of the above"], correct: 3, explain: "Plant cells are distinguished by their cellulose cell walls, chloroplasts for photosynthesis, and large vacuoles." },
            { q: "Factor primarily affecting organism distribution?", options: ["Wind", "Temperature", "Day length", "Soil pH"], correct: 1, explain: "Temperature is a critical abiotic factor that determines the metabolic rates and survival of organisms across biomes." },
            { q: "Sex-linked traits are located on", options: ["Autosomes", "Sex chromosomes", "Mitochondria", "Ribosomes"], correct: 1, explain: "Sex-linked traits (like color blindness) are carried on the X or Y chromosomes." },
            { q: "Main human excretory organ?", options: ["Kidney", "Lung", "Skin", "Liver"], correct: 0, explain: "While others assist, the kidneys are the primary organs for filtering nitrogenous waste from the blood." },
            { q: "NOT a method of reproduction in animals?", options: ["Budding", "Sexual", "Sporulation", "Asexual"], correct: 2, explain: "Sporulation is typical of fungi, bacteria, and some plants, but not commonly found in the animal kingdom." },
            { q: "Truth about viruses:", options: ["Cellular structure", "Living", "Require host to replicate", "Independent reproduction"], correct: 2, explain: "Viruses are obligate intracellular parasites that cannot reproduce outside of a living host cell." },
            { q: "Typical of phylum Arthropoda?", options: ["Bones", "Segmented body", "Closed circulation", "Radial symmetry"], correct: 1, explain: "Arthropods are characterized by segmented bodies, jointed appendages, and a chitinous exoskeleton." }
        ];

        let state = {
            name: "",
            currentIdx: 0,
            answers: {},
            flagged: new Set(),
            timeLeft: 1200,
            timerId: null,
            cheatCount: 0,
            submitted: false,
            startTime: null
        };

        const app = document.getElementById('app');

        function init() {
            renderHome();
            window.addEventListener('blur', () => {
                if (state.startTime && !state.submitted) {
                    state.cheatCount++;
                    document.getElementById('cheat-warning').classList.remove('hidden');
                }
            });
        }

        function dismissCheatWarning() { document.getElementById('cheat-warning').classList.add('hidden'); }

        function renderHome() {
            app.innerHTML = `
                <div class="max-w-4xl mx-auto space-y-8">
                    <header class="text-center space-y-4 py-8">
                        <div class="w-20 h-20 bg-indigo-600 rounded-3xl mx-auto flex items-center justify-center shadow-2xl rotate-3">
                            <i class="fas fa-microscope text-3xl text-white"></i>
                        </div>
                        <h1 class="text-5xl font-extrabold tracking-tight">BEACON BRAINS</h1>
                        <p class="text-indigo-400 font-semibold tracking-widest text-sm uppercase">Biology Specialist Division | Examination Portal</p>
                    </header>

                    <div class="grid lg:grid-cols-5 gap-8">
                        <div class="lg:col-span-3 glass-card rounded-3xl p-8 space-y-6">
                            <h2 class="text-xl font-bold border-b border-slate-800 pb-4">Candidate Identification</h2>
                            <div class="space-y-4">
                                <label class="block">
                                    <span class="text-xs font-bold text-slate-500 uppercase ml-1">Full Examination Name</span>
                                    <input type="text" id="name-in" placeholder="John Doe" 
                                           class="mt-2 w-full bg-slate-900 border border-slate-700 rounded-xl p-4 text-white focus:border-indigo-500 outline-none transition-all font-medium">
                                </label>
                                <div class="grid grid-cols-2 gap-4">
                                    <div class="p-4 bg-slate-900/50 rounded-xl border border-slate-800">
                                        <span class="block text-[10px] text-slate-500 font-bold uppercase">Time Limit</span>
                                        <span class="text-lg font-bold">20 Minutes</span>
                                    </div>
                                    <div class="p-4 bg-slate-900/50 rounded-xl border border-slate-800">
                                        <span class="block text-[10px] text-slate-500 font-bold uppercase">Total Items</span>
                                        <span class="text-lg font-bold">40 Questions</span>
                                    </div>
                                </div>
                                <button onclick="startExam()" class="btn-primary w-full py-5 rounded-2xl font-black text-lg uppercase tracking-widest mt-4">
                                    Initialize Exam
                                </button>
                            </div>
                        </div>

                        <div class="lg:col-span-2 glass-card rounded-3xl p-8 space-y-6 bg-indigo-950/20">
                            <h3 class="text-lg font-bold">Portal Instructions</h3>
                            <div class="space-y-4 text-sm text-slate-400 leading-relaxed">
                                <div class="instruction-item">
                                    <strong class="text-slate-200">Anti-Cheat Enabled:</strong> Leaving the tab or resizing windows will be flagged by proctors.
                                </div>
                                <div class="instruction-item">
                                    <strong class="text-slate-200">Auto-Save:</strong> Your answers are saved locally as you progress through the paper.
                                </div>
                                <div class="instruction-item">
                                    <strong class="text-slate-200">Scientific Tools:</strong> A calculator is provided in the bottom corner of your workspace.
                                </div>
                                <div class="instruction-item">
                                    <strong class="text-slate-200">Review Period:</strong> Comprehensive explanations are available after submission.
                                </div>
                            </div>
                        </div>
                    </div>

                    <footer class="text-center py-10 opacity-30 text-[10px] font-bold tracking-[0.3em] uppercase">
                        © 2026 Beacon Brains Education Authority
                    </footer>
                </div>
            `;
        }

        function startExam() {
            const name = document.getElementById('name-in').value.trim();
            if (!name) return alert("Candidate name is required for registration.");
            state.name = name;
            state.startTime = Date.now();
            document.getElementById('calc-toggle').classList.remove('hidden');
            renderExam();
            startTimer();
        }

        function startTimer() {
            state.timerId = setInterval(() => {
                state.timeLeft--;
                if (state.timeLeft <= 0) finishExam(true);
                else updateTimerUI();
            }, 1000);
        }

        function updateTimerUI() {
            const el = document.getElementById('timer-display');
            if (!el) return;
            const m = Math.floor(state.timeLeft / 60);
            const s = state.timeLeft % 60;
            el.innerText = `${m}:${s.toString().padStart(2, '0')}`;
            if (state.timeLeft < 180) el.classList.add('text-red-500');
        }

        function renderExam() {
            const q = QUESTIONS[state.currentIdx];
            app.innerHTML = `
                <div class="flex flex-col lg:flex-row gap-8">
                    <div class="flex-1 space-y-6">
                        <div class="glass-card rounded-3xl p-8 border-l-8 border-indigo-600 shadow-2xl min-h-[500px] flex flex-col">
                            <div class="flex justify-between items-center mb-10">
                                <span class="bg-indigo-500/10 px-4 py-2 rounded-lg text-xs font-black text-indigo-300 uppercase tracking-widest">
                                    Objective Item ${state.currentIdx + 1}
                                </span>
                                <div id="timer-display" class="text-2xl font-mono font-black text-emerald-400">20:00</div>
                            </div>
                            
                            <h2 class="text-2xl font-bold leading-relaxed mb-10 text-slate-100 flex-grow">${q.q}</h2>
                            
                            <div class="grid gap-4">
                                ${q.options.map((opt, i) => `
                                    <button onclick="pick(${i})" class="group flex items-center w-full p-5 rounded-2xl border transition-all text-left
                                        ${state.answers[state.currentIdx] === i 
                                            ? 'bg-indigo-600 border-indigo-400 shadow-xl' 
                                            : 'bg-slate-900/40 border-slate-800 hover:border-slate-600'}">
                                        <div class="w-10 h-10 rounded-xl bg-slate-900 flex items-center justify-center mr-4 font-black transition-colors">
                                            ${String.fromCharCode(65 + i)}
                                        </div>
                                        <span class="font-semibold text-lg">${opt}</span>
                                    </button>
                                `).join('')}
                            </div>
                        </div>

                        <div class="flex justify-between items-center bg-slate-900/90 p-6 rounded-3xl border border-slate-800">
                            <div class="flex gap-4">
                                <button onclick="move(-1)" class="px-6 py-3 rounded-xl bg-slate-800 hover:bg-slate-700 font-bold disabled:opacity-20" ${state.currentIdx === 0 ? 'disabled' : ''}>
                                    <i class="fas fa-chevron-left"></i>
                                </button>
                                <button onclick="move(1)" class="px-6 py-3 rounded-xl bg-slate-800 hover:bg-slate-700 font-bold disabled:opacity-20" ${state.currentIdx === 39 ? 'disabled' : ''}>
                                    <i class="fas fa-chevron-right"></i>
                                </button>
                            </div>
                            
                            <button onclick="toggleFlag()" class="text-amber-500 font-black px-4 flex items-center">
                                <i class="${state.flagged.has(state.currentIdx) ? 'fas' : 'far'} fa-flag mr-2 text-xl"></i> 
                                <span class="hidden sm:inline">FLAG QUESTION</span>
                            </button>

                            <button onclick="openSubmitModal()" class="px-8 py-3 rounded-xl bg-indigo-600 hover:bg-indigo-500 font-bold shadow-lg shadow-indigo-500/20">
                                <i class="fas fa-paper-plane mr-2"></i> SUBMIT EXAM
                            </button>
                        </div>
                    </div>

                    <div class="w-full lg:w-80 space-y-6">
                        <div class="glass-card rounded-3xl p-6 shadow-xl sticky top-8">
                            <h3 class="text-[10px] font-black text-slate-500 uppercase tracking-widest mb-6">Question Palette</h3>
                            <div class="grid grid-cols-5 gap-3">
                                ${QUESTIONS.map((_, i) => `
                                    <button onclick="jump(${i})" class="palette-btn h-10 rounded-xl text-xs font-black border transition-all
                                        ${state.currentIdx === i ? 'current' : ''}
                                        ${state.answers[i] !== undefined ? 'answered' : 'bg-slate-900/50 text-slate-500 border-slate-800'}
                                        ${state.flagged.has(i) ? 'flagged' : ''}">
                                        ${i + 1}
                                    </button>
                                `).join('')}
                            </div>
                            <div class="mt-8 pt-6 border-t border-slate-800 space-y-4">
                                <div class="flex items-center justify-between text-[10px] font-bold text-slate-500">
                                    <span>PROGRESS</span>
                                    <span>${Object.keys(state.answers).length}/40</span>
                                </div>
                                <div class="h-2 w-full bg-slate-800 rounded-full overflow-hidden">
                                    <div class="h-full bg-indigo-500 transition-all" style="width: ${(Object.keys(state.answers).length/40)*100}%"></div>
                                </div>
                                <button onclick="openSubmitModal()" class="w-full py-4 bg-indigo-600 hover:bg-indigo-500 rounded-2xl font-black uppercase text-[10px] tracking-widest">
                                    Finish Portal Session
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            `;
            updateTimerUI();
        }

        function pick(i) { state.answers[state.currentIdx] = i; renderExam(); }
        function move(dir) { if (state.currentIdx + dir >= 0 && state.currentIdx + dir < 40) { state.currentIdx += dir; renderExam(); } }
        function jump(i) { state.currentIdx = i; renderExam(); }
        function toggleFlag() {
            if (state.flagged.has(state.currentIdx)) state.flagged.delete(state.currentIdx);
            else state.flagged.add(state.currentIdx);
            renderExam();
        }

        function openSubmitModal() {
            const unanswered = 40 - Object.keys(state.answers).length;
            const text = unanswered > 0 ? `You have ${unanswered} unanswered questions.` : "All questions have been attempted.";
            document.getElementById('unanswered-count').innerText = text;
            document.getElementById('submit-modal').classList.remove('hidden');
        }

        function closeSubmitModal() { document.getElementById('submit-modal').classList.add('hidden'); }

        function confirmSubmission() {
            closeSubmitModal();
            finishExam();
        }

        function finishExam(auto = false) {
            if (state.submitted) return;
            clearInterval(state.timerId);
            state.submitted = true;
            let score = 0;
            QUESTIONS.forEach((q, i) => { if (state.answers[i] === q.correct) score++; });
            renderResults(score);
        }

        function renderResults(score) {
            const perc = (score / 40) * 100;
            const timeStr = Math.floor((Date.now() - state.startTime) / 60000);
            
            app.innerHTML = `
                <div class="max-w-2xl mx-auto glass-card rounded-3xl p-12 text-center shadow-2xl mt-10 space-y-10">
                    <header>
                        <h2 class="text-4xl font-black mb-2">RESULTS RELEASED</h2>
                        <p class="text-indigo-400 font-bold uppercase tracking-widest text-xs">Official Examination Certificate</p>
                    </header>
                    
                    <div class="relative w-64 h-64 mx-auto">
                        <svg class="w-full h-full transform -rotate-90" viewBox="0 0 36 36">
                            <circle cx="18" cy="18" r="16" fill="none" stroke="#1e293b" stroke-width="2.5"></circle>
                            <circle cx="18" cy="18" r="16" fill="none" stroke="#6366f1" stroke-width="2.5" 
                                    stroke-dasharray="${perc}, 100" stroke-linecap="round" class="transition-all duration-1000"></circle>
                        </svg>
                        <div class="absolute inset-0 flex flex-col items-center justify-center">
                            <span class="text-7xl font-black">${score}</span>
                            <span class="text-slate-500 font-bold text-sm">TOTAL SCORE</span>
                        </div>
                    </div>

                    <div class="grid grid-cols-2 gap-4">
                        <div class="bg-indigo-500/5 p-6 rounded-3xl border border-indigo-500/10 text-left">
                            <span class="block text-[10px] text-slate-500 uppercase font-black mb-1 tracking-widest">Candidate Name</span>
                            <span class="text-lg font-bold">${state.name}</span>
                        </div>
                        <div class="bg-indigo-500/5 p-6 rounded-3xl border border-indigo-500/10 text-left">
                            <span class="block text-[10px] text-slate-500 uppercase font-black mb-1 tracking-widest">Performance</span>
                            <span class="text-lg font-bold">${perc}%</span>
                        </div>
                    </div>

                    <div class="p-4 bg-slate-900/50 rounded-2xl border border-slate-800 text-xs font-medium text-slate-500 flex items-center justify-between">
                        <span><i class="fas fa-fingerprint mr-2"></i> Time Taken: ${timeStr} mins</span>
                        <span><i class="fas fa-shield-halved mr-2"></i> Violations: ${state.cheatCount}</span>
                    </div>

                    <div class="space-y-4">
                        <button onclick="renderReview()" class="w-full py-5 rounded-2xl btn-primary font-black uppercase text-xs tracking-widest">
                            Review Detailed Performance
                        </button>
                        <button onclick="location.reload()" class="w-full py-4 text-slate-500 hover:text-slate-300 font-bold text-xs uppercase tracking-widest">
                            Return to Portal Login
                        </button>
                    </div>
                </div>
            `;
            document.getElementById('calc-toggle').remove();
        }

        function renderReview() {
            app.innerHTML = `
                <div class="max-w-4xl mx-auto space-y-8">
                    <header class="flex justify-between items-center bg-slate-900/80 p-6 rounded-3xl border border-slate-800 sticky top-4 z-[100] backdrop-blur-md">
                        <div>
                            <h2 class="text-2xl font-black">Performance Review</h2>
                            <p class="text-[10px] text-indigo-400 font-bold uppercase tracking-widest">Post-Examination Feedback</p>
                        </div>
                        <button onclick="location.reload()" class="px-6 py-3 rounded-xl bg-slate-800 hover:bg-slate-700 font-bold text-sm">
                            EXIT REVIEW
                        </button>
                    </header>

                    <div class="space-y-6 pb-20">
                        ${QUESTIONS.map((q, i) => {
                            const isCorrect = state.answers[i] === q.correct;
                            return `
                                <div class="glass-card rounded-3xl p-8 border-l-4 ${isCorrect ? 'border-emerald-500' : 'border-red-500'} relative overflow-hidden">
                                    <div class="absolute top-0 right-0 p-4">
                                        ${isCorrect 
                                            ? '<span class="px-3 py-1 bg-emerald-500/20 text-emerald-400 rounded-full text-[10px] font-black uppercase">Correct</span>'
                                            : '<span class="px-3 py-1 bg-red-500/20 text-red-400 rounded-full text-[10px] font-black uppercase">Incorrect</span>'
                                        }
                                    </div>
                                    
                                    <div class="mb-6">
                                        <span class="text-[10px] font-black text-slate-500 uppercase tracking-widest mb-2 block">Question ${i + 1}</span>
                                        <p class="text-xl font-bold text-slate-100">${q.q}</p>
                                    </div>

                                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-6">
                                        <div class="p-4 rounded-2xl ${state.answers[i] === q.correct ? 'bg-emerald-500/10 border border-emerald-500/20' : 'bg-red-500/10 border border-red-500/20'}">
                                            <span class="block text-[10px] text-slate-500 font-black uppercase mb-1">Your Selection</span>
                                            <span class="font-bold ${state.answers[i] === q.correct ? 'text-emerald-400' : 'text-red-400'}">
                                                ${state.answers[i] !== undefined ? q.options[state.answers[i]] : 'No selection made'}
                                            </span>
                                        </div>
                                        <div class="p-4 rounded-2xl bg-indigo-500/10 border border-indigo-500/20">
                                            <span class="block text-[10px] text-slate-500 font-black uppercase mb-1">Correct Solution</span>
                                            <span class="font-bold text-indigo-300">${q.options[q.correct]}</span>
                                        </div>
                                    </div>

                                    <div class="bg-slate-900/50 p-6 rounded-2xl border border-slate-800">
                                        <h4 class="text-xs font-black text-indigo-400 uppercase tracking-widest mb-3 flex items-center">
                                            <i class="fas fa-lightbulb mr-2"></i> Scientific Explanation
                                        </h4>
                                        <p class="text-sm text-slate-300 leading-relaxed italic">
                                            "${q.explain}"
                                        </p>
                                    </div>
                                </div>
                            `;
                        }).join('')}
                    </div>
                </div>
            `;
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Calculator logic
        let cVal = "";
        function toggleCalculator() { document.getElementById('calc-modal').classList.toggle('hidden'); }
        function calcNum(n) { cVal += n; updateCD(); }
        function calcOp(op) { cVal += " " + op + " "; updateCD(); }
        function calcClear() { cVal = ""; updateCD(); }
        function calcEqual() { 
            try { 
                let res = eval(cVal.replace('×', '*').replace('÷', '/').replace('sqrt', 'Math.sqrt'));
                cVal = Number.isInteger(res) ? res.toString() : res.toFixed(3);
            } catch { cVal = "ERR"; } 
            updateCD(); 
        }
        function updateCD() { document.getElementById('calc-display').value = cVal || "0"; }

        init();
    </script>
</body>
</html>
