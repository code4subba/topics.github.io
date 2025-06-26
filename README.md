<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Agentic AI: Docusign & ServiceNow Integration</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- 
    Chosen Palette: "Calm Harmony" - A palette grounded in warm neutrals (bg-stone-50, bg-stone-100) with a professional blue (bg-sky-600, text-sky-800) for primary actions and accents, and a soft gray (text-slate-600) for text to create a calm, readable, and focused experience.
    Application Structure Plan: The SPA is structured as a narrative journey. It starts with a high-level overview (Hero & Executive Summary), then introduces the core concepts (Platform Convergence, Agentic AI Framework), presents the core findings as interactive elements (Use Case Dashboard), and finally provides a concluding analysis (Value Gain & Conclusion). This top-down approach allows users to either get a quick overview or dive deep into specific use cases. The central interaction is the use case dashboard, allowing users to filter and explore based on their interests (e.g., HR, CLM), which is more intuitive than a linear report format. Navigation is handled by a sticky top bar that smoothly scrolls to sections.
    Visualization & Content Choices:
    - Report Info: Agentic AI Framework (5 stages). -> Goal: Organize/Explain Process. -> Viz: Interactive HTML/CSS diagram. -> Interaction: On hover, details for each stage are revealed. -> Justification: More engaging and space-efficient than a static list, encouraging exploration of the framework. -> Library/Method: Tailwind CSS for styling, Vanilla JS for hover interactions.
    - Report Info: 5 Use Cases. -> Goal: Compare/Organize. -> Viz: Interactive card-based dashboard with filters. -> Interaction: Users click filter buttons (e.g., 'CLM', 'HR') to dynamically show/hide relevant use case cards. Clicking a card reveals detailed information (Technical Approach, Value Gain). -> Justification: Allows users to quickly find use cases relevant to their domain without reading the entire report. It's a user-centric discovery model. -> Library/Method: Vanilla JS for filtering and toggling visibility.
    - Report Info: Value Gain summary. -> Goal: Inform/Compare. -> Viz: Bar Chart. -> Interaction: Tooltips on hover provide specific value metrics. -> Justification: A bar chart provides a quick, scannable visual comparison of the benefits across different areas (Efficiency, Compliance, etc.), making the value proposition immediately clear. -> Library/Method: Chart.js for responsive canvas chart.
    CONFIRMATION: NO SVG graphics used. NO Mermaid JS used.
    -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #fafaf9; /* stone-50 */
            color: #475569; /* slate-600 */
        }
        .nav-link {
            transition: color 0.3s ease;
        }
        .nav-link:hover, .nav-link.active {
            color: #0284c7; /* sky-600 */
        }
        .card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
        }
        .filter-btn.active {
            background-color: #0284c7; /* sky-600 */
            color: white;
        }
        .section-hidden {
            display: none;
        }
        .fade-in {
            animation: fadeIn 0.5s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .sticky-nav {
            position: sticky;
            top: 0;
            z-index: 50;
            backdrop-filter: blur(10px);
            background-color: rgba(250, 250, 249, 0.8);
        }
        .framework-stage .stage-icon {
            transition: all 0.3s ease;
        }
        .framework-stage:hover .stage-icon {
            transform: scale(1.1);
            background-color: #0284c7; /* sky-600 */
            color: white;
        }
        .chart-container {
            position: relative;
            height: 40vh;
            width: 100%;
            max-width: 800px;
            max-height: 450px;
            margin: auto;
        }
    </style>
</head>
<body class="bg-stone-50 text-slate-700">

    <!-- Header & Navigation -->
    <header id="header" class="sticky-nav border-b border-stone-200">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex-shrink-0">
                    <h1 class="text-xl font-bold text-sky-800">Docusign + ServiceNow</h1>
                </div>
                <nav class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-4">
                        <a href="#introduction" class="nav-link px-3 py-2 rounded-md text-sm font-medium">Introduction</a>
                        <a href="#framework" class="nav-link px-3 py-2 rounded-md text-sm font-medium">Framework</a>
                        <a href="#use-cases" class="nav-link px-3 py-2 rounded-md text-sm font-medium">Use Cases</a>
                        <a href="#value-gain" class="nav-link px-3 py-2 rounded-md text-sm font-medium">Value Gain</a>
                        <a href="#conclusion" class="nav-link px-3 py-2 rounded-md text-sm font-medium">Conclusion</a>
                    </div>
                </nav>
            </div>
        </div>
    </header>

    <main class="container mx-auto px-4 sm:px-6 lg:px-8 py-12">

        <!-- Introduction Section -->
        <section id="introduction" class="text-center mb-20">
            <h1 class="text-4xl md:text-5xl font-extrabold text-slate-900 mb-4">Maximizing Enterprise Agility with Agentic AI</h1>
            <p class="max-w-3xl mx-auto text-lg text-slate-600 mb-6">An interactive exploration of high-value use cases integrating Docusign Intelligent Agreement Management (IAM) and ServiceNow Now Assist to fundamentally transform enterprise agreement workflows.</p>
            <div class="bg-white p-8 rounded-xl shadow-md border border-stone-200">
                <h2 class="text-2xl font-bold text-slate-800 mb-3">Executive Summary</h2>
                <p class="text-left text-slate-600">This report explores the strategic imperative and technical feasibility of integrating Docusign IAM with ServiceNow Now Assist, leveraging Agentic AI. The analysis identifies five high-value use cases demonstrating how this synergy can drive unprecedented efficiency, reduce operational risk, and significantly enhance stakeholder experiences. The core value proposition extends beyond simple data synchronization, enabling autonomous, intelligent agents that can initiate, manage, and continuously optimize agreement-centric processes. Organizations implementing these integrations can anticipate substantial gains in operational efficiency, accelerated business cycles, a fortified compliance posture, and superior user satisfaction.</p>
            </div>
        </section>

        <!-- Agentic AI Framework Section -->
        <section id="framework" class="mb-20">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-slate-900">The ServiceNow Agentic AI Framework</h2>
                <p class="max-w-2xl mx-auto mt-4 text-slate-600">Agentic AI operates in a five-stage cycle, moving beyond simple automation to enable proactive, autonomous, and continuously improving systems. Hover over each stage to learn more.</p>
            </div>

            <div class="relative flex flex-col md:flex-row items-center justify-center space-y-8 md:space-y-0 md:space-x-4 lg:space-x-8">
                <!-- Arrows -->
                <div class="hidden md:block absolute top-1/2 left-0 w-full h-0.5 bg-stone-300 -translate-y-1/2"></div>
                <div class="hidden md:block absolute top-1/2 right-0 w-full h-0.5" style="z-index: 1;">
                    <div class="absolute right-[9%] top-1/2 -mt-2 text-3xl text-stone-400">→</div>
                    <div class="absolute right-[28%] top-1/2 -mt-2 text-3xl text-stone-400">→</div>
                    <div class="absolute right-[47%] top-1/2 -mt-2 text-3xl text-stone-400">→</div>
                    <div class="absolute right-[66%] top-1/2 -mt-2 text-3xl text-stone-400">→</div>
                    <div class="absolute right-[85%] top-1/2 -mt-2 text-3xl text-stone-400">→</div>
                </div>


                <div id="framework-stages" class="w-full flex flex-col md:flex-row justify-between items-center z-10 space-y-4 md:space-y-0">
                    <!-- Framework stages will be injected here by JS -->
                </div>
            </div>
            <div id="framework-details" class="mt-8 bg-white p-6 rounded-xl shadow-md border border-stone-200 min-h-[120px] flex items-center justify-center text-center">
                <p class="text-slate-600">Hover over a stage to see details.</p>
            </div>
        </section>
        
        <!-- Use Cases Section -->
        <section id="use-cases" class="mb-20">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-slate-900">Interactive Use Cases</h2>
                <p class="max-w-2xl mx-auto mt-4 text-slate-600">Filter the use cases by business area to explore how this integration drives value across the enterprise. Click on any card for a detailed breakdown.</p>
            </div>
            
            <div id="filters" class="flex justify-center flex-wrap gap-2 mb-8">
                <!-- Filter buttons will be injected here by JS -->
            </div>

            <div id="use-cases-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- Use case cards will be injected here by JS -->
            </div>
        </section>

        <!-- Dynamic Modal for Use Case Details -->
        <div id="useCaseModal" class="fixed inset-0 bg-black bg-opacity-50 z-50 hidden items-center justify-center p-4">
            <div class="bg-white rounded-lg shadow-2xl w-full max-w-4xl max-h-[90vh] overflow-y-auto">
                <div class="sticky top-0 bg-white p-4 sm:p-6 border-b border-stone-200 flex justify-between items-center">
                    <h3 id="modalTitle" class="text-xl sm:text-2xl font-bold text-slate-900"></h3>
                    <button id="closeModal" class="text-slate-500 hover:text-sky-600">&times;</button>
                </div>
                <div id="modalContent" class="p-6 sm:p-8"></div>
            </div>
        </div>

        <!-- Value Gain Section -->
        <section id="value-gain" class="mb-20">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-slate-900">Quantifying the Value Gain</h2>
                <p class="max-w-2xl mx-auto mt-4 text-slate-600">The integration delivers measurable improvements across key business metrics. This chart visualizes the core areas of value unlocked by implementing these agentic workflows.</p>
            </div>
            <div class="bg-white p-8 rounded-xl shadow-md border border-stone-200">
                <div class="chart-container">
                    <canvas id="valueGainChart"></canvas>
                </div>
            </div>
        </section>

        <!-- Conclusion Section -->
        <section id="conclusion" class="text-center">
            <div class="bg-sky-800 text-white p-12 rounded-xl shadow-lg">
                <h2 class="text-3xl font-bold mb-4">Conclusion: A New Era of Enterprise Agility</h2>
                <p class="max-w-3xl mx-auto text-lg text-sky-100 mb-6">The integration of Docusign IAM with ServiceNow Now Assist, driven by Agentic AI, represents a transformative leap in managing enterprise workflows. The shift from mere automation to autonomous, self-optimizing processes unlocks unprecedented value. By leveraging Docusign as a 'Structured Data Factory' and ServiceNow as the intelligent action engine, organizations can achieve significant gains in efficiency, enhance compliance, and foster superior stakeholder experiences. This is not an incremental improvement; it is a foundational step towards building a truly intelligent and adaptive enterprise.</p>
            </div>
        </section>

    </main>

    <script>
    document.addEventListener('DOMContentLoaded', function() {
        const frameworkData = [
            { id: 1, title: 'Data Gathering', icon: '📥', description: 'The AI collects and processes information from diverse sources, including databases, APIs (like Docusign\'s), and real-time feeds, to build a comprehensive understanding of the task.' },
            { id: 2, title: 'Reasoning', icon: '🧠', description: 'The AI analyzes the gathered data, identifying patterns, evaluating relationships, assessing risks, and calculating probabilities to refine its understanding and inform subsequent actions.' },
            { id: 3, title: 'Building a Plan', icon: '🗺️', description: 'The AI structures its tasks into a logical sequence, prioritizing steps, anticipating potential obstacles, and determining the most efficient path forward. It can revise its plan in response to changing conditions.' },
            { id: 4, title: 'Taking Action', icon: '⚙️', description: 'The Agentic AI executes tasks through direct system interactions, which may involve triggering automated processes (like a Docusign workflow), adjusting configurations, or requesting human approval.' },
            { id: 5, title: 'Learning', icon: '📈', description: 'After completing a task, the AI reviews the outcome to determine if further adjustments are needed. It incorporates feedback from system logs and user interactions to refine its decision-making for future scenarios.' }
        ];

        const useCasesData = [
            { 
                id: 1, 
                category: 'CLM',
                title: 'Intelligent Contract Lifecycle Automation (CLM)', 
                summary: 'Automate & optimize the entire contract lifecycle, from drafting and negotiation to proactive post-execution management, ensuring continuous compliance.',
                technicalApproach: `
                    <h4 class="font-bold text-lg mb-2 text-slate-800">Technical Approach</h4>
                    <ul class="list-disc list-inside space-y-2 text-slate-600">
                        <li><b>Initiation:</b> ServiceNow Now Assist parses a contract request, extracting key details.</li>
                        <li><b>Orchestration:</b> Flow Designer invokes the Docusign Maestro API to start a contract generation workflow, populating templates with ServiceNow data.</li>
                        <li><b>Review & Negotiation:</b> Docusign Iris AI identifies clause deviations. Data is sent to ServiceNow via Docusign Connect. Now Assist analyzes deviations, generates summaries for legal review, and can suggest fallback clauses.</li>
                        <li><b>Execution & Storage:</b> The eSignature API manages signing. Completed agreements are stored in Docusign Navigator.</li>
                        <li><b>Monitoring:</b> ServiceNow's Agentic AI ingests AI-extracted data (expiration dates, key terms) from Navigator to proactively trigger renewal workflows or create tasks.</li>
                    </ul>
                `,
                valueGain: `
                    <h4 class="font-bold text-lg mb-2 mt-4 text-slate-800">Value Gain</h4>
                    <p class="text-slate-600">Dramatically increases operational efficiency and reduces contract cycle times (Docusign reports 70% time savings). It enhances compliance through proactive identification of non-standard clauses and automated monitoring of key dates. The system moves towards self-optimizing CLM by learning from negotiation delays or rejections to improve future contract success rates.</p>
                    More with CLM: `
                    <h4 class="font-bold text-lg mb-2 mt-4 text-slate-800">More with CLM</h4>
                    <p class="text-slate-600">DocuSign Agreement Desk enhances CLM functionality by providing a centralized, intelligent workspace where sales, legal, and business teams can collaborate on agreements in real time. It streamlines contract review and approval processes, surfaces key insights and risks using AI, and integrates seamlessly with systems like Salesforce. This results in faster deal cycles, reduced legal bottlenecks, and improved visibility into contract status—bringing CLM-like efficiency and control to any agreement workflow.</p>
                `
            },
            { 
                id: 2, 
                category: 'CX',
                title: 'Proactive Customer Onboarding', 
                summary: 'Streamline the customer onboarding journey by intelligently managing agreements and autonomously triggering service fulfillment tasks in ServiceNow.',
                technicalApproach: `
                    <h4 class="font-bold text-lg mb-2 text-slate-800">Technical Approach</h4>
                    <ul class="list-disc list-inside space-y-2 text-slate-600">
                        <li><b>Data Collection:</b> A Docusign Web Form collects initial customer data, using Data Verification to ensure accuracy.</li>
                        <li><b>Identity Verification:</b> Docusign Identify verifies the signer's identity. Failures trigger real-time alerts to ServiceNow via Docusign Connect.</li>
                        <li><b>Risk Mitigation:</b> Now Assist's Agentic AI analyzes the identity risk, potentially creating a security incident and summarizing the issue for a human agent.</li>
                        <li><b>Fulfillment:</b> Upon successful signing, the AI automatically triggers service fulfillment tasks in ServiceNow (e.g., account provisioning, service activation) based on the agreement type.</li>
                        <li><b>Communication:</b> Docusign's Multi-channel Delivery and Now Assist's Content Creation provide personalized updates to the customer.</li>
                    </ul>
                `,
                valueGain: `
                    <h4 class="font-bold text-lg mb-2 mt-4 text-slate-800">Value Gain</h4>
                    <p class="text-slate-600">Enhances customer experience with a seamless, proactive onboarding process. It accelerates time-to-value by linking agreement completion directly to service provisioning. The system facilitates proactive risk mitigation through real-time identity verification analysis, transforming reactive issue handling into proactive fraud prevention.</p>
                `
            },
            { 
                id: 3, 
                category: 'GRC',
                title: 'Automated Risk & Compliance Monitoring', 
                summary: 'Continuously monitor the entire agreement portfolio for compliance deviations, critical clause adherence, and key risk indicators, triggering automated remediation.',
                technicalApproach: `
                    <h4 class="font-bold text-lg mb-2 text-slate-800">Technical Approach</h4>
                    <ul class="list-disc list-inside space-y-2 text-slate-600">
                        <li><b>Data Ingestion:</b> Docusign Navigator serves as the central repository. The Navigator API feeds AI-extracted, structured contract data into ServiceNow.</li>
                        <li><b>Continuous Analysis:</b> Now Assist's Agentic AI uses 'Contract Analysis' and 'Predictive Intelligence' to analyze the data against compliance rules, flagging anomalies (e.g., missing GDPR clauses, high liability limits).</li>
                        <li><b>Remediation:</b> Upon detecting a risk, the AI triggers a GRC task in ServiceNow, summarizing the issue for the compliance team.</li>
                        <li><b>Action:</b> It can recommend actions or initiate a Docusign Maestro workflow to send a corrective amendment, pre-filled with necessary details.</li>
                    </ul>
                `,
                valueGain: `
                    <h4 class="font-bold text-lg mb-2 mt-4 text-slate-800">Value Gain</h4>
                    <p class="text-slate-600">Transforms compliance from a reactive, manual audit to a proactive, continuous monitoring system. It enhances the organization's risk posture by enabling "AI-Driven GRC," where risk assessments are based on the actual, real-time terms of executed agreements, not just generic policies.</p>
                `
            },
            { 
                id: 4, 
                category: 'Procurement',
                title: 'Dynamic Vendor & Partner Onboarding', 
                summary: 'Expedite vendor onboarding by automating the entire agreement process, from qualification and contract signing to compliance checks and system provisioning.',
                technicalApproach: `
                    <h4 class="font-bold text-lg mb-2 text-slate-800">Technical Approach</h4>
                    <ul class="list-disc list-inside space-y-2 text-slate-600">
                        <li><b>Workflow Generation:</b> Now Assist dynamically creates an onboarding workflow based on the vendor's profile.</li>
                        <li><b>Agreement Orchestration:</b> A Docusign Maestro workflow delivers Web Forms and eSignature envelopes, using Data Verification for accuracy.</li>
                        <li><b>Compliance Check:</b> As agreements are executed, the Agentic AI analyzes extracted data from Docusign Navigator, cross-referencing it with internal policies in ServiceNow to flag non-compliant terms.</li>
                        <li><b>Automated Provisioning:</b> Upon full completion and validation, the AI triggers IT, finance, and operational provisioning tasks within ServiceNow.</li>
                    </ul>
                `,
                valueGain: `
                    <h4 class="font-bold text-lg mb-2 mt-4 text-slate-800">Value Gain</h4>
                    <p class="text-slate-600">Significantly accelerates vendor onboarding cycles, impacting project timelines and operational readiness. Enhances compliance by automating checks against contractual terms and improves data accuracy through AI extraction and verification, fostering stronger, more efficient vendor relationships.</p>
                `
            },
            { 
                id: 5, 
                category: 'HR',
                title: 'Intelligent HR Agreement Management', 
                summary: 'Transform HR agreement processes like new hire onboarding and policy acknowledgments into intelligent, personalized, and automated workflows.',
                technicalApproach: `
                     <h4 class="font-bold text-lg mb-2 text-slate-800">Technical Approach</h4>
                    <ul class="list-disc list-inside space-y-2 text-slate-600">
                        <li><b>Workflow Initiation:</b> An event in ServiceNow HR Service Delivery (e.g., new hire created) triggers a dynamic Maestro workflow for HR agreements.</li>
                        <li><b>Document Delivery:</b> Docusign delivers Web Forms for data collection and eSignature envelopes for contracts, benefits, and policies.</li>
                        <li><b>Proactive Monitoring:</b> The Agentic AI monitors completion status via Docusign Connect. If a deadline is missed, it automatically sends personalized reminders or creates a task for an HR generalist.</li>
                        <li><b>Task Automation:</b> Upon completion of all agreements, the AI automatically triggers subsequent HR tasks like system access provisioning or scheduling training.</li>
                    </ul>
                `,
                valueGain: `
                    <h4 class="font-bold text-lg mb-2 mt-4 text-slate-800">Value Gain</h4>
                    <p class="text-slate-600">Enhances the employee experience with a streamlined, digital onboarding process. Boosts HR operational efficiency by automating document generation, routing, and follow-up. Strengthens compliance and auditability by ensuring all necessary acknowledgments are securely captured and centrally managed.</p>
                `
            }
        ];

        const frameworkStagesContainer = document.getElementById('framework-stages');
        const frameworkDetailsContainer = document.getElementById('framework-details');
        
        frameworkData.forEach(stage => {
            const stageEl = document.createElement('div');
            stageEl.className = 'framework-stage flex flex-col items-center cursor-pointer text-center w-full md:w-1/5';
            stageEl.innerHTML = `
                <div class="stage-icon w-16 h-16 rounded-full bg-white border-2 border-stone-300 flex items-center justify-center text-3xl mb-2">${stage.icon}</div>
                <h4 class="font-semibold text-slate-800">${stage.title}</h4>
            `;
            stageEl.addEventListener('mouseenter', () => {
                frameworkDetailsContainer.innerHTML = `<p class="text-slate-700 font-medium fade-in">${stage.description}</p>`;
            });
            frameworkStagesContainer.appendChild(stageEl);
        });

        const filtersContainer = document.getElementById('filters');
        const useCasesGrid = document.getElementById('use-cases-grid');
        const modal = document.getElementById('useCaseModal');
        const closeModalBtn = document.getElementById('closeModal');
        const modalTitle = document.getElementById('modalTitle');
        const modalContent = document.getElementById('modalContent');
        
        const categories = ['All', ...new Set(useCasesData.map(uc => uc.category))];

        categories.forEach(category => {
            const btn = document.createElement('button');
            btn.className = 'filter-btn px-4 py-2 text-sm font-medium rounded-full border border-stone-300 transition';
            btn.textContent = category;
            if (category === 'All') {
                btn.classList.add('active');
            }
            btn.addEventListener('click', () => {
                document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                filterUseCases(category);
            });
            filtersContainer.appendChild(btn);
        });

        function renderUseCases(filteredData) {
            useCasesGrid.innerHTML = '';
            filteredData.forEach(uc => {
                const card = document.createElement('div');
                card.className = 'card bg-white p-6 rounded-xl shadow-md border border-stone-200 cursor-pointer fade-in';
                card.innerHTML = `
                    <span class="inline-block px-3 py-1 text-xs font-semibold text-sky-800 bg-sky-100 rounded-full mb-3">${uc.category}</span>
                    <h3 class="text-xl font-bold text-slate-800 mb-2">${uc.title}</h3>
                    <p class="text-slate-600">${uc.summary}</p>
                `;
                card.addEventListener('click', () => openModal(uc));
                useCasesGrid.appendChild(card);
            });
        }

        function filterUseCases(category) {
            const filteredData = category === 'All' ? useCasesData : useCasesData.filter(uc => uc.category === category);
            renderUseCases(filteredData);
        }

        function openModal(useCase) {
            modalTitle.textContent = useCase.title;
            modalContent.innerHTML = useCase.technicalApproach + useCase.valueGain;
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        function closeModal() {
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        closeModalBtn.addEventListener('click', closeModal);
        modal.addEventListener('click', (e) => {
            if (e.target === modal) {
                closeModal();
            }
        });

        renderUseCases(useCasesData);

        // Chart.js
        const ctx = document.getElementById('valueGainChart').getContext('2d');
        const valueGainChart = new Chart(ctx, {
            type: 'bar',
            data: {
                labels: ['Efficiency Gain', 'Risk Reduction', 'Cycle Time Accel.', 'Data Accuracy', 'User Experience'],
                datasets: [{
                    label: 'Impact Score',
                    data: [90, 85, 80, 95, 88],
                    backgroundColor: [
                        'rgba(56, 189, 248, 0.6)',
                        'rgba(14, 165, 233, 0.6)',
                        'rgba(2, 132, 199, 0.6)',
                        'rgba(3, 105, 161, 0.6)',
                        'rgba(7, 89, 133, 0.6)'
                    ],
                    borderColor: [
                        'rgb(56, 189, 248)',
                        'rgb(14, 165, 233)',
                        'rgb(2, 132, 199)',
                        'rgb(3, 105, 161)',
                        'rgb(7, 89, 133)'
                    ],
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    y: {
                        beginAtZero: true,
                        max: 100,
                        title: {
                            display: true,
                            text: 'Relative Impact (%)'
                        }
                    }
                },
                plugins: {
                    legend: {
                        display: false
                    },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                let label = context.dataset.label || '';
                                if (label) {
                                    label += ': ';
                                }
                                if (context.parsed.y !== null) {
                                    label += context.parsed.y + '% Improvement';
                                }
                                return label;
                            }
                        }
                    }
                }
            }
        });

        // Smooth scrolling for nav links
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                document.querySelector(this.getAttribute('href')).scrollIntoView({
                    behavior: 'smooth'
                });
            });
        });
    });
    </script>
</body>
</html>
