<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Optimizing Procurement: An Interactive Guide</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutrals & Slate Blue -->
    <!-- Application Structure Plan: The SPA is designed as an interactive dashboard, moving away from the linear structure of the source report. The goal is to create an exploratory user flow. It starts with a high-level, interactive visualization of the core problem (The Vicious Cycle). Users can then navigate via a sticky header to deeper, thematic sections: 'The Diagnosis' to explore the challenges, 'The Optimization Toolkit' to interact with solutions, 'Strategic Levers' to see the impact of these solutions, and 'Technology Enablers' to learn about supporting tools. This structure groups related concepts logically, allowing users to explore based on their interests (e.g., "What are the problems?" vs. "How do we fix them?") rather than forcing a linear reading. This non-linear, task-oriented design enhances usability and understanding by making complex information digestible and explorable. -->
    <!-- Visualization & Content Choices: The application translates the report's text and tables into interactive components. Goal: 'Understand the core problem' -> Viz: Interactive circular diagram (HTML/CSS/JS) showing the 'Vicious Cycle' of procurement issues. Interaction: Clicking a stage reveals detailed text. Justification: Visually represents the report's core analogy, making the interconnectedness immediately clear. Goal: 'Compare Challenges' -> Viz: Donut chart for Spend Under Management (Chart.js) and info cards. Interaction: Hovering provides data, clicking reveals details. Justification: Quantifies the scale of the problems discussed in Section II of the report. Goal: 'Explore Solutions' -> Viz: Interactive diagrams for invoice matching and KPI bar chart (Chart.js). Interaction: Buttons change the matching diagram; chart tooltips provide KPI details. Justification: Simplifies complex processes (matching) and makes performance data (KPIs) easy to compare. Goal: 'See Impact' -> Viz: Dynamic stat cards. Interaction: Toggle updates stats to show a 'before/after' scenario. Justification: Clearly demonstrates the value and ROI of the proposed strategies. All visualizations use Canvas, HTML, and CSS, adhering to the NO SVG/Mermaid constraint. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #F8F7F4;
            color: #1a202c;
        }
        .nav-link {
            transition: color 0.3s, border-bottom-color 0.3s;
            border-bottom: 2px solid transparent;
        }
        .nav-link:hover, .nav-link.active {
            color: #2c5282;
            border-bottom-color: #2c5282;
        }
        .content-section {
            display: none;
        }
        .content-section.active {
            display: block;
        }
        .cycle-node {
            transition: all 0.3s ease-in-out;
            cursor: pointer;
        }
        .cycle-node:hover, .cycle-node.active {
            transform: scale(1.05);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
        .tab-button {
            transition: all 0.2s ease-in-out;
        }
        .tab-button.active {
            background-color: #4A5568;
            color: white;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .fade-in {
            animation: fadeIn 0.5s ease-in-out forwards;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .tech-card {
            transition: transform 0.3s, box-shadow 0.3s;
        }
        .tech-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }
        .stat-card-value {
             transition: color 0.5s ease-in-out;
        }
    </style>
</head>
<body class="antialiased">

    <header id="main-header" class="bg-white/80 backdrop-blur-lg sticky top-0 z-50 shadow-md">
        <nav class="container mx-auto px-6 py-3 flex justify-between items-center">
            <h1 class="text-xl md:text-2xl font-bold text-gray-800">Procurement Optimization</h1>
            <div class="hidden md:flex space-x-8">
                <a href="#cycle" data-section="cycle" class="nav-link pb-1">The Vicious Cycle</a>
                <a href="#diagnosis" data-section="diagnosis" class="nav-link pb-1">The Diagnosis</a>
                <a href="#toolkit" data-section="toolkit" class="nav-link pb-1">The Optimization Toolkit</a>
                <a href="#levers" data-section="levers" class="nav-link pb-1">Strategic Levers</a>
                <a href="#tech" data-section="tech" class="nav-link pb-1">Technology Enablers</a>
            </div>
            <div class="md:hidden">
                <select id="mobile-nav" class="block w-full bg-gray-200 border border-gray-200 text-gray-700 py-2 px-3 pr-8 rounded-lg leading-tight focus:outline-none focus:bg-white focus:border-gray-500">
                    <option value="cycle">The Vicious Cycle</option>
                    <option value="diagnosis">The Diagnosis</option>
                    <option value="toolkit">The Optimization Toolkit</option>
                    <option value="levers">Strategic Levers</option>
                    <option value="tech">Technology Enablers</option>
                </select>
            </div>
        </nav>
    </header>

    <main class="container mx-auto px-6 py-8 md:py-12">

        <section id="cycle" class="content-section min-h-[80vh] flex flex-col items-center justify-center">
            <div class="text-center mb-12">
                <h2 class="text-3xl md:text-4xl font-bold text-gray-800 mb-2">The Vicious Cycle of Procurement Inefficiency</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto">Transactional errors cascade into strategic failures. Click each stage to understand how small issues create significant financial blind spots.</p>
            </div>
            <div class="w-full flex flex-col lg:flex-row items-center justify-between gap-8">
                <div class="w-full lg:w-1/2">
                    <div class="grid grid-cols-2 gap-4 md:gap-6">
                        <div id="node-po" class="cycle-node bg-white p-4 md:p-6 rounded-xl shadow-lg border border-gray-200 text-center">
                            <div class="text-4xl mb-2">📄</div>
                            <h3 class="font-semibold text-sm md:text-base">Unmatched POs</h3>
                        </div>
                        <div class="flex items-center justify-center text-3xl text-gray-400">→</div>
                        <div class="flex items-center justify-center text-3xl text-gray-400 lg:hidden">↓</div>
                        <div class="flex items-center justify-center text-3xl text-gray-400">↓</div>

                        <div id="node-contracts" class="cycle-node bg-white p-4 md:p-6 rounded-xl shadow-lg border border-gray-200 text-center">
                            <div class="text-4xl mb-2">📝</div>
                            <h3 class="font-semibold text-sm md:text-base">Underused Contracts</h3>
                        </div>
                        <div class="flex items-center justify-center text-3xl text-gray-400 lg:hidden">←</div>
                        
                         <div id="node-spots" class="cycle-node bg-white p-4 md:p-6 rounded-xl shadow-lg border border-gray-200 text-center">
                            <div class="text-4xl mb-2">❓</div>
                            <h3 class="font-semibold text-sm md:text-base">Spend Blind Spots</h3>
                        </div>
                        <div class="flex items-center justify-center text-3xl text-gray-400">↑</div>
                        <div class="flex items-center justify-center text-3xl text-gray-400 lg:hidden">↑</div>
                        <div class="flex items-center justify-center text-3xl text-gray-400">←</div>

                        <div id="node-savings" class="cycle-node bg-white p-4 md:p-6 rounded-xl shadow-lg border border-gray-200 text-center">
                            <div class="text-4xl mb-2">💸</div>
                            <h3 class="font-semibold text-sm md:text-base">Missed Savings</h3>
                        </div>
                    </div>
                </div>
                <div class="w-full lg:w-1/2 mt-8 lg:mt-0">
                    <div id="cycle-details" class="bg-white p-6 rounded-xl shadow-lg min-h-[300px] fade-in">
                        <h3 id="detail-title" class="text-xl font-bold text-gray-800 mb-4"></h3>
                        <p id="detail-text" class="text-gray-600 leading-relaxed"></p>
                    </div>
                </div>
            </div>
        </section>

        <section id="diagnosis" class="content-section">
             <div class="text-center mb-12">
                <h2 class="text-3xl md:text-4xl font-bold text-gray-800 mb-2">The Diagnosis: Quantifying the Challenges</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto">This section provides a deeper look into the core challenges identified in the report. The visualizations below illustrate the scale of these issues, from poor contract management to the vast, unmanaged 'tail spend' that creates risks and financial leakage.</p>
            </div>
            <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
                <div class="lg:col-span-1 md:col-span-2 bg-white p-6 rounded-xl shadow-lg">
                    <h3 class="text-xl font-bold text-gray-800 mb-2">Spend Under Management</h3>
                    <p class="text-gray-600 mb-4 text-sm">A large portion of spend is often 'maverick' or unmanaged, leading to missed savings. This chart shows a typical scenario.</p>
                    <div class="chart-container h-64 md:h-72">
                        <canvas id="spendChart"></canvas>
                    </div>
                </div>
                 <div class="lg:col-span-2 md:col-span-2 bg-white p-6 rounded-xl shadow-lg flex flex-col">
                     <h3 class="text-xl font-bold text-gray-800 mb-4">Core Problem Areas</h3>
                     <div class="flex-grow grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="bg-gray-50 p-4 rounded-lg">
                            <h4 class="font-semibold text-gray-700">Contract Leakage</h4>
                            <p class="text-sm text-gray-600 mt-1">Value erosion from non-compliance with negotiated terms. The IACCM estimates this can cost companies up to <span class="font-bold text-blue-800">9% of annual revenue</span>.</p>
                        </div>
                        <div class="bg-gray-50 p-4 rounded-lg">
                            <h4 class="font-semibold text-gray-700">Maverick Spend</h4>
                            <p class="text-sm text-gray-600 mt-1">Purchases made outside of approved channels. This directly fuels contract underutilization and increases costs and risks.</p>
                        </div>
                        <div class="bg-gray-50 p-4 rounded-lg">
                            <h4 class="font-semibold text-gray-700">Tail Spend Inefficiency</h4>
                             <p class="text-sm text-gray-600 mt-1">The 80% of transactions that make up 20% of spend are often unmanaged, hiding significant savings opportunities and compliance risks.</p>
                        </div>
                        <div class="bg-gray-50 p-4 rounded-lg">
                            <h4 class="font-semibold text-gray-700">Poor Data Quality</h4>
                             <p class="text-sm text-gray-600 mt-1">Fragmented and inaccurate data across siloed systems is the root cause of spend blind spots, making strategic decisions impossible.</p>
                        </div>
                     </div>
                </div>
            </div>
        </section>

        <section id="toolkit" class="content-section">
             <div class="text-center mb-12">
                <h2 class="text-3xl md:text-4xl font-bold text-gray-800 mb-2">The Optimization Toolkit</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto">This toolkit provides interactive explanations of the key solutions outlined in the report. Explore how systematic invoice analysis and robust contract compliance form the foundation of a high-performing procurement function.</p>
            </div>
            <div class="bg-white p-6 rounded-xl shadow-lg">
                <div class="flex justify-center border-b border-gray-200 mb-6">
                    <button data-tab="invoice" class="tab-button py-2 px-6 font-semibold text-gray-600 active">Invoice Analysis</button>
                    <button data-tab="compliance" class="tab-button py-2 px-6 font-semibold text-gray-600">Contract Compliance</button>
                </div>
                <div id="tab-content-invoice">
                    <div class="grid md:grid-cols-2 gap-8 items-center">
                        <div>
                            <h3 class="text-xl font-bold text-gray-800 mb-2">Invoice Matching Explained</h3>
                            <p class="text-gray-600 mb-4">Invoice matching is the first line of defense against discrepancies. The rigor can be adapted based on risk. Select a method to see how it works.</p>
                            <div class="flex space-x-2 mb-4">
                                <button data-match="2" class="match-btn bg-blue-100 text-blue-800 py-1 px-3 rounded-full text-sm font-semibold">2-Way</button>
                                <button data-match="3" class="match-btn bg-gray-200 text-gray-700 py-1 px-3 rounded-full text-sm font-semibold">3-Way</button>
                                <button data-match="4" class="match-btn bg-gray-200 text-gray-700 py-1 px-3 rounded-full text-sm font-semibold">4-Way</button>
                            </div>
                            <div id="match-diagram" class="flex flex-col space-y-2">
                                <div id="doc-po" class="match-doc flex items-center bg-green-50 p-3 rounded-lg border border-green-200">📄 Purchase Order</div>
                                <div class="text-2xl text-center">+</div>
                                <div id="doc-invoice" class="match-doc flex items-center bg-green-50 p-3 rounded-lg border border-green-200">🧾 Invoice</div>
                                <div id="doc-grn" class="match-doc hidden flex items-center bg-green-50 p-3 rounded-lg border border-green-200">📦 Goods Receipt</div>
                                <div id="doc-qa" class="match-doc hidden flex items-center bg-green-50 p-3 rounded-lg border border-green-200">✅ Quality Report</div>
                            </div>
                        </div>
                        <div class="text-center p-4 bg-gray-50 rounded-lg">
                             <h4 id="match-title" class="text-lg font-bold text-gray-800">2-Way Matching</h4>
                             <p id="match-desc" class="text-gray-600 mt-2">Verifies that invoice details (quantity, price) match the purchase order. Ensures the purchase was authorized. Ideal for services or low-risk recurring purchases.</p>
                        </div>
                    </div>
                </div>
                <div id="tab-content-compliance" class="hidden">
                    <h3 class="text-xl font-bold text-gray-800 mb-2 text-center">Tracking Key Performance Indicators (KPIs)</h3>
                    <p class="text-gray-600 mb-6 text-center max-w-2xl mx-auto">Continuous monitoring of KPIs is essential for ensuring contracts deliver their negotiated value. This chart visualizes critical compliance and utilization metrics.</p>
                    <div class="chart-container h-80">
                        <canvas id="kpiChart"></canvas>
                    </div>
                </div>
            </div>
        </section>

        <section id="levers" class="content-section">
            <div class="text-center mb-12">
                <h2 class="text-3xl md:text-4xl font-bold text-gray-800 mb-2">Strategic Levers for Transformation</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto">With data-driven insights, procurement can pull powerful strategic levers. This section illustrates the tangible impact of optimization on cash flow, supplier value, and contract strength. Toggle to see the 'before' and 'after' effect.</p>
            </div>
            <div class="flex justify-center mb-8">
                 <label for="impact-toggle" class="flex items-center cursor-pointer">
                    <span class="mr-3 font-semibold text-gray-700">Before Optimization</span>
                    <div class="relative">
                        <input type="checkbox" id="impact-toggle" class="sr-only">
                        <div class="block bg-gray-300 w-14 h-8 rounded-full"></div>
                        <div class="dot absolute left-1 top-1 bg-white w-6 h-6 rounded-full transition"></div>
                    </div>
                    <span class="ml-3 font-semibold text-blue-800">After Optimization</span>
                </label>
            </div>
            <div class="grid md:grid-cols-3 gap-8">
                <div class="bg-white p-6 rounded-xl shadow-lg text-center">
                    <h3 class="font-semibold text-gray-700">Payment Terms</h3>
                    <p id="stat-payment" class="text-4xl font-bold my-4 stat-card-value text-red-600">Net 30</p>
                    <p id="desc-payment" class="text-sm text-gray-600">Standard terms, no early payment discounts captured.</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-lg text-center">
                    <h3 class="font-semibold text-gray-700">Supplier Performance</h3>
                    <p id="stat-performance" class="text-4xl font-bold my-4 stat-card-value text-red-600">Reactive</p>
                    <p id="desc-performance" class="text-sm text-gray-600">Issues addressed only after they cause disruptions.</p>
                </div>
                <div class="bg-white p-6 rounded-xl shadow-lg text-center">
                    <h3 class="font-semibold text-gray-700">Contract Value</h3>
                    <p id="stat-contract" class="text-4xl font-bold my-4 stat-card-value text-red-600">Fragmented</p>
                    <p id="desc-contract" class="text-sm text-gray-600">Spend spread across many suppliers, limiting negotiation leverage.</p>
                </div>
            </div>
        </section>

        <section id="tech" class="content-section">
             <div class="text-center mb-12">
                <h2 class="text-3xl md:text-4xl font-bold text-gray-800 mb-2">Technology Enablers</h2>
                <p class="text-lg text-gray-600 max-w-3xl mx-auto">Modern technology is the catalyst for procurement excellence. These platforms automate processes, provide deep insights, and empower strategic decision-making. Click each card to learn more.</p>
            </div>
            <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
                <div class="tech-card bg-white p-6 rounded-xl shadow-lg border border-gray-200">
                    <h3 class="font-bold text-lg text-gray-800">Procure-to-Pay (P2P)</h3>
                    <p class="text-sm text-gray-600 mt-2">Automates the entire purchasing lifecycle, from requisition to payment, ensuring upstream compliance.</p>
                </div>
                <div class="tech-card bg-white p-6 rounded-xl shadow-lg border border-gray-200">
                    <h3 class="font-bold text-lg text-gray-800">Contract Lifecycle (CLM)</h3>
                    <p class="text-sm text-gray-600 mt-2">Manages contracts as dynamic assets, improving visibility, compliance, and value realization.</p>
                </div>
                <div class="tech-card bg-white p-6 rounded-xl shadow-lg border border-gray-200">
                    <h3 class="font-bold text-lg text-gray-800">Spend Analytics</h3>
                    <p class="text-sm text-gray-600 mt-2">Transforms raw data into actionable intelligence, illuminating blind spots and savings opportunities.</p>
                </div>
                <div class="tech-card bg-white p-6 rounded-xl shadow-lg border border-gray-200">
                    <h3 class="font-bold text-lg text-gray-800">AI / Machine Learning</h3>
                    <p class="text-sm text-gray-600 mt-2">Augments human intelligence by detecting patterns, predicting trends, and automating complex analysis.</p>
                </div>
            </div>
        </section>

    </main>
    
    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const sections = document.querySelectorAll('.content-section');
            const navLinks = document.querySelectorAll('.nav-link');
            const mobileNav = document.getElementById('mobile-nav');

            const cycleData = {
                po: {
                    title: 'Unmatched Purchase Orders',
                    text: 'An unmatched Purchase Order (PO) signals a breakdown at the start of the procure-to-pay cycle. This failure in transactional accuracy means purchases are made without proper linkage to pre-negotiated agreements, representing a failure to align the purchasing document with subsequent transactions.'
                },
                contracts: {
                    title: 'Underused Contracts',
                    text: 'When POs are unmatched, it often means existing contracts with favorable terms and pricing remain underutilized. This disconnect between strategic sourcing and operational purchasing leads to value erosion and missed savings.'
                },
                savings: {
                    title: 'Missed Savings',
                    text: 'The direct financial consequence of underused contracts and maverick spending. Failure to channel purchases through negotiated agreements means missing out on volume discounts, rebates, and better pricing, representing a tangible financial loss.'
                },
                spots: {
                    title: 'Spend Blind Spots',
                    text: 'The foundational problem that allows other issues to persist. When an organization cannot see its expenditures clearly across all categories and suppliers, it cannot identify or capitalize on savings opportunities, creating a cycle of inefficiency.'
                }
            };

            const impactData = {
                before: {
                    payment: { value: 'Net 30', desc: 'Standard terms, no early payment discounts captured.' , color: 'text-red-600'},
                    performance: { value: 'Reactive', desc: 'Issues addressed only after they cause disruptions.', color: 'text-red-600' },
                    contract: { value: 'Fragmented', desc: 'Spend spread across many suppliers, limiting negotiation leverage.', color: 'text-red-600' }
                },
                after: {
                    payment: { value: 'Dynamic', desc: 'Capturing early payment discounts and optimizing cash flow.', color: 'text-green-600' },
                    performance: { value: 'Proactive', desc: 'Data-driven SPM identifies issues before they escalate.', color: 'text-green-600' },
                    contract: { value: 'Consolidated', desc: 'Leveraging total spend volume for better terms and stronger partnerships.', color: 'text-green-600' }
                }
            };
            
            function updateActiveSection(sectionId) {
                sections.forEach(section => {
                    section.classList.toggle('active', section.id === sectionId);
                });
                navLinks.forEach(link => {
                    link.classList.toggle('active', link.dataset.section === sectionId);
                });
                if(mobileNav.value !== sectionId) {
                    mobileNav.value = sectionId;
                }
            }

            function handleNavClick(e) {
                e.preventDefault();
                const sectionId = e.target.dataset.section;
                updateActiveSection(sectionId);
                document.getElementById(sectionId).scrollIntoView({ behavior: 'smooth' });
            }

            navLinks.forEach(link => link.addEventListener('click', handleNavClick));
            
            mobileNav.addEventListener('change', (e) => {
                const sectionId = e.target.value;
                updateActiveSection(sectionId);
                document.getElementById(sectionId).scrollIntoView({ behavior: 'smooth' });
            });


            const cycleNodes = document.querySelectorAll('.cycle-node');
            const detailTitle = document.getElementById('detail-title');
            const detailText = document.getElementById('detail-text');
            const cycleDetailsContainer = document.getElementById('cycle-details');

            function updateCycleDetails(nodeId) {
                const key = nodeId.split('-')[1];
                const data = cycleData[key];
                
                cycleDetailsContainer.classList.remove('fade-in');

                setTimeout(() => {
                    detailTitle.textContent = data.title;
                    detailText.textContent = data.text;
                    cycleDetailsContainer.classList.add('fade-in');
                }, 10);

                cycleNodes.forEach(node => {
                    node.classList.toggle('active', node.id === `node-${key}`);
                });
            }

            cycleNodes.forEach(node => {
                node.addEventListener('click', () => {
                    updateCycleDetails(node.id);
                });
            });

            updateCycleDetails('node-po');

            const tabButtons = document.querySelectorAll('.tab-button');
            const tabContents = {
                invoice: document.getElementById('tab-content-invoice'),
                compliance: document.getElementById('tab-content-compliance')
            };

            tabButtons.forEach(button => {
                button.addEventListener('click', () => {
                    const tabId = button.dataset.tab;
                    tabButtons.forEach(btn => btn.classList.toggle('active', btn.dataset.tab === tabId));
                    Object.values(tabContents).forEach(content => content.classList.add('hidden'));
                    tabContents[tabId].classList.remove('hidden');
                    tabContents[tabId].classList.add('fade-in');
                });
            });
            
            const matchButtons = document.querySelectorAll('.match-btn');
            const matchDocs = {
                po: document.getElementById('doc-po'),
                invoice: document.getElementById('doc-invoice'),
                grn: document.getElementById('doc-grn'),
                qa: document.getElementById('doc-qa')
            };
            const matchTitle = document.getElementById('match-title');
            const matchDesc = document.getElementById('match-desc');
            const matchInfo = {
                '2': { title: '2-Way Matching', desc: 'Verifies that invoice details (quantity, price) match the purchase order. Ensures the purchase was authorized. Ideal for services or low-risk recurring purchases.', docs: ['po', 'invoice'] },
                '3': { title: '3-Way Matching', desc: 'Adds the Goods Receipt Note (GRN) to confirm items were not only ordered but also received before payment. Standard for tangible goods.', docs: ['po', 'invoice', 'grn'] },
                '4': { title: '4-Way Matching', desc: 'The most stringent method, adding a Quality/Inspection Report to ensure goods meet required standards before payment. Used for critical, high-value items.', docs: ['po', 'invoice', 'grn', 'qa'] }
            }

            matchButtons.forEach(button => {
                button.addEventListener('click', () => {
                    const matchType = button.dataset.match;
                    
                    matchButtons.forEach(btn => {
                        btn.classList.remove('bg-blue-100', 'text-blue-800');
                        btn.classList.add('bg-gray-200', 'text-gray-700');
                    });
                    button.classList.add('bg-blue-100', 'text-blue-800');
                    button.classList.remove('bg-gray-200', 'text-gray-700');

                    Object.values(matchDocs).forEach(doc => doc.classList.add('hidden'));
                    
                    const info = matchInfo[matchType];
                    matchTitle.textContent = info.title;
                    matchDesc.textContent = info.desc;
                    info.docs.forEach(docKey => {
                        matchDocs[docKey].classList.remove('hidden');
                        matchDocs[docKey].classList.add('fade-in');
                    });
                });
            });


            const spendCtx = document.getElementById('spendChart').getContext('2d');
            new Chart(spendCtx, {
                type: 'doughnut',
                data: {
                    labels: ['Spend Under Management', 'Maverick Spend', 'Tail Spend'],
                    datasets: [{
                        label: 'Spend Distribution',
                        data: [65, 20, 15],
                        backgroundColor: ['#4A5568', '#A0AEC0', '#E2E8F0'],
                        borderColor: '#F8F7F4',
                        borderWidth: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'bottom' },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return `${context.label}: ${context.raw}%`;
                                }
                            }
                        }
                    }
                }
            });
            
            const kpiCtx = document.getElementById('kpiChart').getContext('2d');
            new Chart(kpiCtx, {
                type: 'bar',
                data: {
                    labels: ['Contract Compliance', 'Contract Utilization', 'PO Accuracy', 'Invoice Accuracy'],
                    datasets: [{
                        label: 'Performance (%)',
                        data: [82, 75, 91, 85],
                        backgroundColor: '#4A5568',
                        borderRadius: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    indexAxis: 'y',
                    scales: {
                        x: {
                            beginAtZero: true,
                            max: 100
                        }
                    },
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return `${context.dataset.label}: ${context.raw}%`;
                                }
                            }
                        }
                    }
                }
            });

            const impactToggle = document.getElementById('impact-toggle');
            const statPayment = document.getElementById('stat-payment');
            const descPayment = document.getElementById('desc-payment');
            const statPerformance = document.getElementById('stat-performance');
            const descPerformance = document.getElementById('desc-performance');
            const statContract = document.getElementById('stat-contract');
            const descContract = document.getElementById('desc-contract');

            impactToggle.addEventListener('change', () => {
                const state = impactToggle.checked ? 'after' : 'before';
                const data = impactData[state];
                
                statPayment.textContent = data.payment.value;
                descPayment.textContent = data.payment.desc;
                statPayment.className = `text-4xl font-bold my-4 stat-card-value ${data.payment.color}`;

                statPerformance.textContent = data.performance.value;
                descPerformance.textContent = data.performance.desc;
                statPerformance.className = `text-4xl font-bold my-4 stat-card-value ${data.performance.color}`;
                
                statContract.textContent = data.contract.value;
                descContract.textContent = data.contract.desc;
                statContract.className = `text-4xl font-bold my-4 stat-card-value ${data.contract.color}`;
            });

            let currentSection = window.location.hash.substring(1) || 'cycle';
            updateActiveSection(currentSection);

            window.addEventListener('scroll', () => {
                let current = 'cycle';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop;
                    if(pageYOffset >= sectionTop - 100){
                        current = section.getAttribute('id');
                    }
                });
                if(current !== (mobileNav.value || navLinks[0].dataset.section)){
                    updateActiveSection(current);
                }
            });

        });
    </script>
</body>
</html>
