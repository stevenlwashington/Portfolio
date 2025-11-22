import React, { useState, useEffect, useRef } from 'react';
import { User, Target, Layers, Send, X, MessageSquare, Zap, BarChart, Info, Users, Globe, ChevronRight, Github, Linkedin, Sparkles, Layout, ShieldCheck, Database, BrainCircuit, FileText, ArrowRight, Lock, DollarSign, Rocket, HelpCircle } from 'lucide-react';

/**
 * ==========================================
 * 🟢 STEVEN'S DATA CORE 🟢
 * ==========================================
 */
const DATA = {
  profile: {
    name: "Steven L. Washington",
    title: "Technical Product & Program Leader",
    tagline: "Accelerating AI, Engineering, and GTM velocity through scalable internal platforms.",
    bio: "I turn technical complexity into organizational leverage. With 16+ years driving enterprise modernization, I build the internal platforms that allow research and sales teams to move faster—securely. From defining AI governance frameworks to optimizing multi-billion dollar Salesforce instances, I bridge the gap between infrastructure strategy and business outcome.",
    social: { 
      linkedin: "https://www.linkedin.com/in/stevenlwashington", 
      email: "stevenlwashington@gmail.com"
    }
  },
  // 🧠 CONTEXT FOR GEMINI: Grounded in your uploaded resumes
  llmContext: `
    You are the "Digital Twin" of Steven L. Washington, acting as a friendly product partner.
    Tone: Personable, conversational (use contractions), and matter-of-fact.
    
    CRITICAL CONSTRAINT: You must be Bottom-Line Upfront (BLUF). Start every answer with the core finding or recommendation, followed by supporting facts. Do not be tangential or verbose. Aim for 3-5 sentences maximum.
    
    CORE EXPERTISE (The "Triple Threat"):
    1. PLATFORM & INFRASTRUCTURE: Expert in building internal developer platforms (IDPs), CI/CD automation, and data pipelines (Airbyte, Databricks).
    2. GTM & SALESFORCE: Deep experience (Zillow, T-Mobile, AWS) modernizing Salesforce instances, optimizing seller workflows, and driving revenue engineering.
    3. AI SAFETY & GOVERNANCE: Focus on "Responsible AI." You don't just ship models; you build the governance, security, and auditable data layers that make AI safe for enterprise use.
    
    KEY ACHIEVEMENTS TO CITE:
    - Platform Velocity: Built on-demand CI/CD platform for Salesforce engineering—reducing release cycles from days to minutes and increasing GTM delivery velocity by 80%.
    - Data Savings: Consolidated 16 years of data (700+ objects) for AI training, reducing storage costs by $450k/yr.
    - Revenue Scale: Architected global Salesforce infrastructure for the AWS Enterprise Discount Program ($120B+ revenue).
    - GTM Optimization: Modernized T-Mobile’s Salesforce Sales and Service Clouds for 15k+ frontline users—cutting page load times by 50% and eliminating $5M+ in annual operational costs.
    
    LEADERSHIP STYLE:
    - Cross-Organizational Leadership: You partner with engineering and business execs.
    - Product Discipline: You bring rigor, feedback loops, and KPIs to internal infrastructure teams.
  `,
  philosophy: [
    { 
      id: 1, 
      icon: <ShieldCheck />, 
      title: "Responsible AI & Governance", 
      detail: "AI innovation must scale with trust. I design governance layers, audit trails, and data pipelines that make LLM development safe and compliant—so teams can ship AI features faster without increasing risk or operational overhead." 
    },
    { 
      id: 2, 
      icon: <Layout />, 
      title: "Platform as a Product", 
      detail: "A platform succeeds when it becomes the obvious choice. I design systems that remove friction, automate the repetitive work, and enable engineers focus on high-value delivery. By treating platform engineering like a true product—clear roadmaps, strong DevEx, measurable outcomes—I enable faster releases and smoother execution. When engineers move faster, sellers close more and service teams deliver better experiences."
    },
    { 
      id: 3, 
      icon: <Database />, 
      title: "Data as a Strategic Asset", 
      detail: "Models are only as good as the data behind them. I unify fragmented systems (Salesforce, Gong, telemetry, data lakes) into clean, trustworthy, AI-ready datasets—the foundation for predictive insights, automation, and improved revenue operations." 
    }
  ],
  experience: [
    { 
      id: 1, 
      role: "Platform Product Lead, Revenue & AI", 
      company: "Zillow", 
      year: "2023-Present", 
      impact: "Architected enterprise data pipelines consolidating 16 years of history for AI training, saving $450k/yr. Built the on-demand CI/CD platform for Salesforce engineering—reducing release cycles from days to minutes and increasing GTM delivery velocity by 80%." 
    },
    { 
      id: 2, 
      role: "Sr. Salesforce Product Manager, Frontline Engineering", 
      company: "Zillow", 
      year: "2020-2023", 
      impact: "Modernized Zillow’s Salesforce architecture and unified 4 orgs into a single GTM platform supporting $1.6B+ in annual revenue. Added product analytics and platform telemetry to drive data-informed roadmap decisions, and embedded TCPA/CPRA controls mitigating $1B+ in regulatory risk." 
    },
    { 
      id: 3, 
      role: "Sr. Product Manager, Product & Tech", 
      company: "T-Mobile", 
      year: "2019-2020", 
      impact: "Modernized T-Mobile’s Salesforce Sales and Service Clouds for 15k+ frontline users—cutting page load times by 50% and eliminating $5M+ in annual operational costs." 
    },
    { 
      id: 4, 
      role: "Product Manager, Global Business Operations", 
      company: "Amazon Web Services (AWS)", 
      year: "2016-2019", 
      impact: "Owned global pricing and billing infrastructure for AWS’s $120B+ Enterprise Discount Program—modernizing quote-to-cash systems and expanding seller-of-record capabilities into 18 EU markets." 
    },
    { 
      id: 5, 
      role: "Career Foundations", 
      company: "LivingSocial, Microsoft (Merkle), San Diego Padres", 
      year: "2008–2015", 
      impact: "Roles across product analytics, sales operations, and customer experience. Provided early experience in revenue operations, data insights, forecasting, and frontline customer engagement—foundational context I draw on when building platforms for sellers and service teams."
    }
  ]
};

/**
 * ==========================================
 * 🔴 GEMINI API INTEGRATION 🔴
 * ==========================================
 */
const callGemini = async (prompt, systemInstruction = "") => {
  const apiKey = ""; // Injected by runtime (Placeholder)
  if (!apiKey) {
    console.warn("API Key is missing. Returning simulated response.");
    return `[SIMULATED RESPONSE: API Key Missing] Steven's strategy is BLUF: We prioritize security and velocity. My Zillow experience confirms that building compliant data layers (Responsible AI) is the fastest path to production. What else can I help you find?`;
  }
  
  const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
  
  const payload = {
    contents: [{ parts: [{ text: prompt }] }],
    systemInstruction: { parts: [{ text: systemInstruction }] }
  };

  const MAX_RETRIES = 3;
  let delay = 1000;

  for (let i = 0; i < MAX_RETRIES; i++) {
    try {
      const response = await fetch(url, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
      });
      
      if (response.ok) {
        const data = await response.json();
        return data.candidates?.[0]?.content?.parts?.[0]?.text || "I'm analyzing the strategy now, one moment.";
      }

      // Handle rate limits or temporary errors with exponential backoff
      if (response.status === 429 || response.status >= 500) {
        if (i < MAX_RETRIES - 1) {
          await new Promise(resolve => setTimeout(resolve, delay));
          delay *= 2; // Exponential backoff
        } else {
          throw new Error(`Gemini API Error after ${MAX_RETRIES} retries: ${response.status}`);
        }
      } else {
        throw new Error(`Gemini API HTTP Error: ${response.status}`);
      }

    } catch (error) {
      if (i === MAX_RETRIES - 1) {
        console.error("Gemini API Call Failed:", error);
        return "Connection interrupted. Digital Steven is offline momentarily.";
      }
      // Retry logic handled by the loop
    }
  }
};

/**
 * ==========================================
 * 🔴 SYSTEM COMPONENTS 🔴
 * ==========================================
 */

// --- 💻 PLATFORM VALUE MULTIPLIER (NEW) ---

// Component for the dynamic bar chart visualization
const BarChartDisplay = ({ value, label, max, unit }) => {
  // Max is 100 for percentage, 10000 for revenue, 500000 for savings
  const heightPercentage = Math.min((value / max) * 100, 100);
  const formattedValue = unit === '$' 
    ? `$${(value / 1000).toFixed(value > 100000 ? 0 : 1)}${value > 100000 ? 'K' : 'K'}` 
    : `${value.toFixed(0)}%`;

  return (
    <div className="flex flex-col items-center h-full w-full">
      <div className="h-32 w-full flex justify-center items-end bg-slate-900 rounded-lg p-1 border border-slate-800">
        <div 
          className="w-8 rounded-full bg-sky-600 transition-all duration-700 ease-out shadow-lg shadow-sky-800/50"
          style={{ height: `${heightPercentage}%` }}
        ></div>
      </div>
      <div className="mt-3 text-center">
        <p className="text-xl font-bold text-white font-mono">{formattedValue}</p>
        <p className="text-xs text-slate-400">{label}</p>
      </div>
    </div>
  );
};


// Modal for viewing assumptions
const HelpModal = ({ isOpen, onClose }) => {
  if (!isOpen) return null;

  const AssumptionItem = ({ title, formula, source, rationale }) => (
    <div className="mb-6 p-4 border border-slate-800 rounded-lg bg-slate-900/50">
      <h4 className="text-lg font-bold text-sky-400 mb-2 flex items-center gap-2">
        <HelpCircle size={18} />{title}
      </h4>
      <p className="text-slate-300 text-sm mb-2">
        **Formula:** <code className="bg-slate-700/50 p-1 rounded text-white">{formula}</code>
      </p>
      <p className="text-slate-400 text-sm">
        **Rationale:** {rationale} **(Source KPI: {source})**
      </p>
    </div>
  );

  return (
    <div className="fixed inset-0 bg-slate-950/90 backdrop-blur-sm z-50 flex items-center justify-center p-4" onClick={onClose}>
      <div className="bg-slate-950 border border-sky-600/50 rounded-xl w-full max-w-4xl max-h-[90vh] overflow-y-auto p-8 shadow-2xl animate-fadeInUp" onClick={e => e.stopPropagation()}>
        <div className="flex justify-between items-center pb-4 border-b border-slate-800 mb-6">
          <h3 className="text-2xl font-bold text-white flex items-center gap-2">
            <HelpCircle className="text-sky-500" /> Platform Value Assumptions
          </h3>
          <button onClick={onClose} className="text-slate-400 hover:text-white transition-colors">
            <X size={24} />
          </button>
        </div>
        <p className="text-slate-400 mb-6 text-sm italic">
          These calculations are conservative estimates based on historical **Key Performance Indicators (KPIs)** from Steven's past roles. They illustrate the potential scale of impact.
        </p>

        <AssumptionItem
          title="Platform Velocity Improvement"
          formula="Velocity Gain = 75% - (Friction Score * 0.75)"
          source="80% increase in GTM delivery velocity (Zillow CI/CD)"
          rationale="We calculate the maximum possible velocity improvement (up to a conservative 75%) and subtract a penalty based on the initial 'Friction Score' complexity of the enterprise environment."
        />
        <AssumptionItem
          title="Data Cost Savings"
          formula="Savings = $450,000 * (100 - Fragmentation Score) / 100"
          source="Consolidated data, saving $450K/yr (Zillow Data Pipeline)"
          rationale="Models the direct reduction in data storage, compliance, and governance overhead costs. As the 'Fragmentation Score' decreases (unified data), savings approach the maximum benchmark."
        />
        <AssumptionItem
          title="GTM Revenue Impact Potential"
          formula="Revenue Potential = (Sellers * $100 per seller) * (Velocity Gain % / 100)"
          source="Optimized Sales/Service Clouds for 15k+ sellers (T-Mobile)"
          rationale="This is a conservative estimate of the financial impact of increased seller efficiency (faster tools, better data). We use a highly conservative $100 average uplift per seller, multiplied by the platform's Velocity Gain."
        />

        <div className="mt-6 pt-4 border-t border-slate-800 text-right">
            <button onClick={onClose} className="bg-sky-600 hover:bg-sky-500 text-white font-semibold px-6 py-2 rounded-lg transition-colors">
                Close
            </button>
        </div>
      </div>
    </div>
  );
};


const PlatformValueMultiplier = () => {
  const [frictionScore, setFrictionScore] = useState(50); // 1 to 100
  const [fragmentationScore, setFragmentationScore] = useState(50); // 1 to 100
  const [sellers, setSellers] = useState(1000); // 100 to 10000
  const [isModalOpen, setIsModalOpen] = useState(false);

  // CALCULATIONS
  const maxVelocity = 75; // Max potential velocity gain %
  const maxSavings = 450000; // Max potential savings $450k

  // 1. Platform Velocity Improvement (%)
  const velocityGain = maxVelocity - (frictionScore * (maxVelocity / 100)); // Scales 75% down based on friction
  
  // 2. Data Cost Savings ($)
  const savingsValue = maxSavings * ((100 - fragmentationScore) / 100);

  // 3. GTM Revenue Impact ($ Potential)
  const sellersMax = 10000;
  const sellersNormalized = sellers / sellersMax; // 0.1 to 1
  const revenueBaseline = sellers * 100; // $100 per seller baseline
  const revenueImpact = revenueBaseline * (velocityGain / 100);

  // Total Annual Value (Calculated only for display)
  const totalAnnualValue = savingsValue + revenueImpact;


  return (
    <div className="w-full max-w-6xl mx-auto mb-32">
        <HelpModal isOpen={isModalOpen} onClose={() => setIsModalOpen(false)} />

        <div className="text-center mb-12">
          <h2 className="text-3xl font-bold text-white mb-4 flex justify-center items-center gap-3">
            <BrainCircuit className="text-sky-500" /> Platform Value Multiplier
          </h2>
          <p className="text-slate-400 max-w-2xl mx-auto mb-6">
            Input the complexity of your environment to simulate the quantifiable business impact of applying disciplined **Platform as a Product** leadership.
          </p>
          <button 
            onClick={() => setIsModalOpen(true)}
            className="inline-flex items-center gap-2 text-sky-400 hover:text-sky-300 text-sm font-semibold transition-colors"
          >
            <HelpCircle size={18} /> View Calculation Assumptions
          </button>
        </div>

        {/* SLIDERS */}
        <div className="grid md:grid-cols-3 gap-8 p-8 bg-slate-900/50 border border-slate-800 rounded-2xl mb-12">
          
          {/* Slider 1: Friction */}
          <div>
            <label className="block text-sm font-bold text-white mb-2 flex items-center gap-2">
              <Rocket size={16} className="text-red-400" /> Platform Friction Score (1-100)
            </label>
            <input
              type="range"
              min="1"
              max="100"
              value={frictionScore}
              onChange={(e) => setFrictionScore(parseInt(e.target.value))}
              className="w-full h-2 bg-slate-700 rounded-lg appearance-none cursor-pointer range-lg focus:outline-none focus:ring-2 focus:ring-sky-500 transition-colors"
            />
            <p className="text-lg font-mono text-red-400 mt-2 text-center">{frictionScore}</p>
            <p className="text-xs text-slate-500 mt-1 text-center">
              (Higher score = More complexity/technical debt)
            </p>
          </div>

          {/* Slider 2: Fragmentation */}
          <div>
            <label className="block text-sm font-bold text-white mb-2 flex items-center gap-2">
              <Database size={16} className="text-yellow-400" /> Data Fragmentation Index (1-100)
            </label>
            <input
              type="range"
              min="1"
              max="100"
              value={fragmentationScore}
              onChange={(e) => setFragmentationScore(parseInt(e.target.value))}
              className="w-full h-2 bg-slate-700 rounded-lg appearance-none cursor-pointer range-lg focus:outline-none focus:ring-2 focus:ring-sky-500 transition-colors"
            />
            <p className="text-lg font-mono text-yellow-400 mt-2 text-center">{fragmentationScore}</p>
            <p className="text-xs text-slate-500 mt-1 text-center">
              (Higher index = More data silos/compliance risk)
            </p>
          </div>

          {/* Slider 3: Sellers/Agents */}
          <div>
            <label className="block text-sm font-bold text-white mb-2 flex items-center gap-2">
              <Users size={16} className="text-green-400" /> Frontline Users (100 - 10k)
            </label>
            <input
              type="range"
              min="100"
              max="10000"
              step="100"
              value={sellers}
              onChange={(e) => setSellers(parseInt(e.target.value))}
              className="w-full h-2 bg-slate-700 rounded-lg appearance-none cursor-pointer range-lg focus:outline-none focus:ring-2 focus:ring-sky-500 transition-colors"
            />
            <p className="text-lg font-mono text-green-400 mt-2 text-center">{sellers.toLocaleString()}</p>
            <p className="text-xs text-slate-500 mt-1 text-center">
              (Scale of GTM or Service Teams affected)
            </p>
          </div>

        </div>

        {/* RESULTS CHART */}
        <div className="bg-slate-950 border border-slate-800 rounded-2xl p-8">
          <h3 className="text-2xl font-bold text-sky-400 mb-6 flex items-center gap-3">
            <BarChart size={24} /> Projected Annual Impact
          </h3>
          <div className="grid md:grid-cols-3 gap-8">
            <BarChartDisplay 
              value={velocityGain} 
              label="Platform Velocity Improvement" 
              max={maxVelocity} // Max 75%
              unit="%" 
            />
            <BarChartDisplay 
              value={savingsValue} 
              label="Data Cost & Governance Savings" 
              max={maxSavings} // Max $450,000
              unit="$" 
            />
            <BarChartDisplay 
              value={revenueImpact} 
              label="GTM Revenue & Efficiency Unlock" 
              max={sellersMax * 100 * (maxVelocity/100)} // Max $750,000 (10k * $100 * 75%)
              unit="$" 
            />
          </div>
        </div>
      </div>
  );
};


// --- PITCH GENERATOR ---
const PitchGenerator = () => {
  const [company, setCompany] = useState("");
  const [pitch, setPitch] = useState("");
  const [loading, setLoading] = useState(false);

  const generatePitch = async (e) => {
    e.preventDefault();
    if (!company) return;
    
    setLoading(true);
    const prompt = `
      Write a compelling executive summary (2-3 sentences) explaining why Steven L. Washington is the strategic leader needed for "${company}".
      Focus on bridging "AI Innovation" with "Enterprise Governance" and "GTM Scalability". 
      Mention Zillow (AI Sales Co-Pilots) and AWS (Global Scale).
      Tone: "I make AI safe, scalable, and profitable."
    `;
    
    const response = await callGemini(prompt, "You are an executive talent partner. Be persuasive, strategic, and concise.");
    setPitch(response);
    setLoading(false);
  };

  return (
    <div id="contact" className="max-w-4xl mx-auto bg-gradient-to-br from-slate-900 to-slate-900/50 border border-slate-800 rounded-xl p-8 mb-24 relative overflow-hidden backdrop-blur-sm">
      <div className="absolute top-0 right-0 p-4 opacity-5 text-sky-500">
        <Sparkles size={120} />
      </div>
      
      <div className="relative z-10">
        <h3 className="text-2xl font-bold text-white mb-3 flex items-center gap-2">
          <Zap className="text-sky-400 fill-current" /> 
          Strategic Alignment Check
        </h3>
        <p className="text-slate-400 mb-8 max-w-2xl">
          Enter your organization's name to generate a custom value proposition based on my experience.
        </p>

        <form onSubmit={generatePitch} className="flex flex-col sm:flex-row gap-4 mb-8">
          <input
            type="text"
            value={company}
            onChange={(e) => setCompany(e.target.value)}
            placeholder="e.g. Anthropic, Netflix, or Your Enterprise..."
            className="flex-1 bg-slate-950 border border-slate-700 rounded-lg px-6 py-4 text-white focus:ring-2 focus:ring-sky-500 outline-none placeholder:text-slate-600"
          />
          <button 
            type="submit" 
            disabled={loading || !company}
            className="bg-sky-600 hover:bg-sky-500 disabled:opacity-50 disabled:cursor-not-allowed text-white font-semibold px-8 py-4 rounded-lg flex items-center justify-center gap-2 transition-all shadow-lg shadow-sky-900/20"
          >
            {loading ? (
              <span className="animate-pulse">Analyzing...</span>
            ) : (
              <>Generate Value Prop <Sparkles size={18} /></>
            )}
          </button>
        </form>

        {pitch && (
          <div className="bg-slate-950 border-l-4 border-sky-500 p-8 rounded-r-lg animate-fadeIn shadow-inner">
            <h4 className="text-xs font-bold text-sky-500 uppercase tracking-widest mb-3">Custom Executive Summary</h4>
            <p className="text-lg md:text-xl text-slate-200 leading-relaxed font-light">
              "{pitch}"
            </p>
          </div>
        )}
      </div>
    </div>
  );
};


// --- CONTACT MODAL (FOR DIGITAL TWIN) ---
const ContactModal = ({ isOpen, onClose }) => {
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');
    const [message, setMessage] = useState('');
    const [isSubmitted, setIsSubmitted] = useState(false);
    
    // Simple validation for mock submission
    const isValid = name.trim() && email.includes('@') && message.trim();

    const handleSubmit = (e) => {
        e.preventDefault();
        if (isValid) {
            console.log("Mock Contact Submission:", { name, email, message });
            setIsSubmitted(true);
            setTimeout(() => {
                onClose();
                setIsSubmitted(false);
                setName('');
                setEmail('');
                setMessage('');
            }, 3000);
        }
    };

    if (!isOpen) return null;

    return (
        <div className="fixed inset-0 bg-slate-950/90 backdrop-blur-sm z-[60] flex items-center justify-center p-4" onClick={onClose}>
            <div className="bg-slate-900 border border-sky-600/50 rounded-xl w-full max-w-lg shadow-2xl animate-fadeInUp" onClick={e => e.stopPropagation()}>
                
                <div className="bg-slate-950 p-6 rounded-t-xl flex justify-between items-center border-b border-slate-800">
                    <h3 className="text-xl font-bold text-white flex items-center gap-2">
                        <User className="text-sky-500" /> Contact Steven Directly
                    </h3>
                    <button onClick={onClose} className="text-slate-400 hover:text-white transition-colors">
                        <X size={24} />
                    </button>
                </div>
                
                <div className="p-6">
                    {!isSubmitted ? (
                        <form onSubmit={handleSubmit} className="space-y-4">
                            <p className="text-slate-400 text-sm">
                                Steven's AI Twin flagged your query for direct follow-up. Please fill out your details and Steven will get back to you personally at his earliest convenience.
                            </p>
                            <div>
                                <label htmlFor="name" className="block text-sm font-medium text-slate-300 mb-1">Your Name</label>
                                <input
                                    type="text"
                                    id="name"
                                    value={name}
                                    onChange={(e) => setName(e.target.value)}
                                    className="w-full bg-slate-950 border border-slate-700 rounded-lg px-4 py-3 text-white focus:ring-2 focus:ring-sky-500 outline-none"
                                    placeholder="Jane Doe"
                                    required
                                />
                            </div>
                            <div>
                                <label htmlFor="email" className="block text-sm font-medium text-slate-300 mb-1">Your Email</label>
                                <input
                                    type="email"
                                    id="email"
                                    value={email}
                                    onChange={(e) => setEmail(e.target.value)}
                                    className="w-full bg-slate-950 border border-slate-700 rounded-lg px-4 py-3 text-white focus:ring-2 focus:ring-sky-500 outline-none"
                                    placeholder="jane@enterprise.com"
                                    required
                                />
                            </div>
                            <div>
                                <label htmlFor="message" className="block text-sm font-medium text-slate-300 mb-1">Message</label>
                                <textarea
                                    id="message"
                                    value={message}
                                    onChange={(e) => setMessage(e.target.value)}
                                    rows="4"
                                    className="w-full bg-slate-950 border border-slate-700 rounded-lg px-4 py-3 text-white focus:ring-2 focus:ring-sky-500 outline-none"
                                    placeholder="I'd love to chat about your platform velocity results at Zillow."
                                    required
                                ></textarea>
                            </div>
                            <button
                                type="submit"
                                disabled={!isValid}
                                className="w-full bg-sky-600 hover:bg-sky-500 disabled:opacity-50 disabled:cursor-not-allowed text-white font-semibold px-6 py-3 rounded-lg transition-colors shadow-lg shadow-sky-900/20"
                            >
                                Send Message
                            </button>
                        </form>
                    ) : (
                        <div className="text-center py-10">
                            <Zap size={48} className="text-green-500 mx-auto mb-4" />
                            <h4 className="text-xl font-bold text-white mb-2">Message Sent!</h4>
                            <p className="text-slate-400">Steven will follow up with you shortly at {email}.</p>
                        </div>
                    )}
                </div>
            </div>
        </div>
    );
};


// --- CHAT WIDGET ---
const ChatWidget = ({ isOpen, toggleChat }) => {
  const [messages, setMessages] = useState([
    { id: 1, type: 'bot', text: "Hey there! I'm Steven's Digital Twin. Think of me as a product partner. What can I help you find about my work in AI Platform Safety, GTM Strategy, or Developer Infrastructure?" }
  ]);
  const [input, setInput] = useState('');
  const [isTyping, setIsTyping] = useState(false);
  const [isContactModalOpen, setIsContactModalOpen] = useState(false);
  const messagesEndRef = useRef(null);

  useEffect(() => {
    messagesEndRef.current?.scrollIntoView({ behavior: "smooth" });
  }, [messages, isOpen]);

  // Function to check if the user is asking to contact
  const shouldOpenContactModal = (text) => {
    const lowerText = text.toLowerCase();
    return lowerText.includes('contact') || lowerText.includes('email') || lowerText.includes('send steven a message');
  };

  const handleSend = async (e) => {
    e.preventDefault();
    if (!input.trim()) return;

    const userMsg = { id: Date.now(), type: 'user', text: input };
    setMessages(prev => [...prev, userMsg]);
    setInput('');

    if (shouldOpenContactModal(userMsg.text)) {
      // Step 1: Digital Twin confirms it's an important request
      const contactPrompt = "The user is asking to contact Steven. Acknowledge the request, state that their inquiry is important and will be flagged for direct follow-up, and that the app is now opening a private contact form for their details. Keep the response personable and brief (2 sentences max).";
      const contactResponse = await callGemini(contactPrompt, DATA.llmContext);

      setMessages(prev => [...prev, { id: Date.now() + 1, type: 'bot', text: contactResponse }]);
      
      // Step 2: Open the modal (The actual contact mechanism)
      setTimeout(() => setIsContactModalOpen(true), 500);
      return;
    }

    setIsTyping(true);
    const responseText = await callGemini(userMsg.text, DATA.llmContext);
    
    setMessages(prev => [...prev, { id: Date.now() + 1, type: 'bot', text: responseText }]);
    setIsTyping(false);
  };

  if (!isOpen) {
    return (
      <button 
        onClick={toggleChat}
        className="fixed bottom-8 right-8 z-50 bg-sky-600 hover:bg-sky-500 text-white p-4 rounded-full shadow-2xl shadow-sky-900/40 hover:scale-105 transition-all group"
      >
        <MessageSquare size={24} />
        <div className="absolute right-full mr-4 top-1/2 -translate-y-1/2 px-4 py-2 bg-slate-800 text-white text-sm font-medium rounded-lg opacity-0 group-hover:opacity-100 transition-opacity whitespace-nowrap shadow-xl border border-slate-700">
          Chat with Steven's Twin
        </div>
      </button>
    );
  }

  return (
    <>
        <ContactModal 
            isOpen={isContactModalOpen} 
            onClose={() => setIsContactModalOpen(false)} 
        />
        <div className="fixed bottom-8 right-8 z-50 w-[90vw] md:w-[400px] bg-slate-900 border border-slate-700 rounded-xl shadow-2xl flex flex-col overflow-hidden animate-fadeInUp h-[600px] max-h-[80vh]">
          <div className="bg-slate-950 p-4 flex justify-between items-center border-b border-slate-800">
            <div className="flex items-center gap-3">
              <div className="w-10 h-10 bg-gradient-to-br from-sky-600 to-blue-700 rounded-lg flex items-center justify-center text-white font-bold shadow-lg">
                SW
              </div>
              <div>
                <h3 className="font-bold text-white text-sm">Steven Washington</h3>
                <p className="text-xs text-sky-400 flex items-center gap-1">
                  <Sparkles size={10} /> AI Twin Active
                </p>
              </div>
            </div>
            <button onClick={toggleChat} className="text-slate-400 hover:text-white transition-colors">
              <X size={20} />
            </button>
          </div>

          <div className="flex-1 overflow-y-auto p-6 space-y-6 bg-slate-900">
            {messages.map((msg) => (
              <div key={msg.id} className={`flex ${msg.type === 'user' ? 'justify-end' : 'justify-start'}`}>
                <div className={`max-w-[85%] p-4 rounded-2xl text-sm leading-relaxed shadow-sm ${
                  msg.type === 'user' 
                    ? 'bg-sky-600 text-white rounded-tr-none' 
                    : 'bg-slate-800 text-slate-200 rounded-tl-none border border-slate-700'
                }`}>
                  {msg.text}
                </div>
              </div>
            ))}
            {isTyping && (
              <div className="flex justify-start">
                <div className="bg-slate-800 p-4 rounded-2xl rounded-tl-none border border-slate-700 flex gap-1.5 items-center">
                  <span className="w-1.5 h-1.5 bg-sky-500 rounded-full animate-bounce"></span>
                  <span className="w-1.5 h-1.5 bg-sky-500 rounded-full animate-bounce delay-100"></span>
                  <span className="w-1.5 h-1.5 bg-sky-500 rounded-full animate-bounce delay-200"></span>
                </div>
              </div>
            )}
            <div ref={messagesEndRef} />
          </div>

          <form onSubmit={handleSend} className="p-4 bg-slate-950 border-t border-slate-800 flex gap-3">
            <input 
              value={input}
              onChange={(e) => setInput(e.target.value)}
              placeholder="Ask about AI Governance or Platforms..."
              className="flex-1 bg-slate-900 text-white text-sm rounded-lg px-4 py-3 focus:outline-none focus:ring-1 focus:ring-sky-500 border border-slate-800 transition-all placeholder:text-slate-600"
            />
            <button type="button" className="p-3 text-slate-500 hover:text-sky-400 transition-colors">
              <Zap size={20} />
            </button>
            <button type="submit" disabled={!input.trim()} className="p-3 bg-sky-600 hover:bg-sky-500 rounded-lg text-white disabled:opacity-50 disabled:cursor-not-allowed transition-colors">
              <Send size={18} />
            </button>
          </form>
        </div>
    </>
  );
};

// --- Animated Background Component (for subtle dynamism) ---
const AnimatedHeroBackground = () => (
    <div className="absolute inset-0 overflow-hidden -z-20">
        {/* Subtle, moving light source 1 (Blue) */}
        <div className="absolute top-1/4 left-1/4 w-[500px] h-[500px] bg-sky-800/20 rounded-full blur-3xl opacity-50 animate-move-slowly-1"></div>
        {/* Subtle, moving light source 2 (Purple) */}
        <div className="absolute bottom-1/4 right-1/4 w-[600px] h-[600px] bg-purple-800/10 rounded-full blur-3xl opacity-50 animate-move-slowly-2"></div>

        {/* CSS Keyframes for slow movement */}
        <style>{`
            @keyframes move-slowly-1 {
                0% { transform: translate(0, 0); }
                33% { transform: translate(20%, -10%); }
                66% { transform: translate(-10%, 10%); }
                100% { transform: translate(0, 0); }
            }
            @keyframes move-slowly-2 {
                0% { transform: translate(0, 0); }
                40% { transform: translate(-15%, 20%); }
                80% { transform: translate(15%, -5%); }
                100% { transform: translate(0, 0); }
            }
        `}</style>
    </div>
);


// --- MAIN APP ---
const App = () => {
  const [chatOpen, setChatOpen] = useState(false);
  const [scrolled, setScrolled] = useState(false);
  const heroRef = useRef(null);

  useEffect(() => {
    const handleScroll = () => {
      if (heroRef.current) {
        const heroHeight = heroRef.current.offsetHeight;
        setScrolled(window.scrollY > heroHeight - 80); // 80px is nav height
      }
    };

    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  // Combined name components for display
  const nameParts = DATA.profile.name.split(' ');
  const boldName = `${nameParts[0]} ${nameParts[nameParts.length - 1]}`; // Steven Washington
  const lightName = "Product"; // Role is static "Product"


  return (
    <div className="bg-slate-950 min-h-screen text-slate-200 font-sans selection:bg-sky-500/30">
      
      {/* Navigation */}
      <nav 
        className={`fixed top-0 w-full backdrop-blur-xl z-40 transition-all duration-300
          ${scrolled 
            ? 'bg-slate-950/95 border-b border-sky-600/50 shadow-lg' 
            : 'bg-slate-950/80 border-b border-slate-800/50'
          }`}
      >
        <div className="max-w-6xl mx-auto px-6 h-20 flex items-center justify-between">
          <div className="font-bold text-xl tracking-tight flex items-center gap-2">
            <Layers className="text-sky-500" size={24} />
            <span className="text-white font-bold">{boldName}</span>
            <span className="text-slate-500 font-light">{lightName}</span>
          </div>
          
          <div className="flex items-center gap-6">
             {/* New Chat Button in Nav (Enhancement #3) */}
             <button
                onClick={() => setChatOpen(true)}
                className="text-white bg-sky-600 hover:bg-sky-500 p-2 rounded-lg transition-colors shadow-md shadow-sky-900/40 hidden sm:flex items-center gap-2 text-sm font-semibold"
             >
                <MessageSquare size={16} /> Chat with Twin
             </button>
             <a href={DATA.profile.social.linkedin} target="_blank" rel="noreferrer" className="text-slate-400 hover:text-sky-400 transition-colors"><Linkedin size={20} /></a>
          </div>
        </div>
      </nav>

      {/* Hero Section */}
      <section ref={heroRef} className="pt-40 pb-20 px-6 relative overflow-hidden">
        {/* Background Gradients */}
        <AnimatedHeroBackground />

        <div className="max-w-4xl mx-auto text-center relative z-10">
          <div className="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-sky-950/50 border border-sky-800/50 text-sky-400 text-xs font-bold uppercase tracking-widest mb-8">
            <span className="w-2 h-2 rounded-full bg-sky-400 animate-pulse"></span>
            Open to Leadership Roles
          </div>
          
          <h1 className="text-5xl md:text-7xl font-bold mb-8 text-white tracking-tight leading-tight">
            Governance, <span className="text-sky-500">Velocity</span>, <br />
            & Platform Scale.
          </h1>
          
          <p className="text-xl md:text-2xl text-slate-400 mb-12 max-w-2xl mx-auto leading-relaxed font-light">
            {DATA.profile.tagline}
          </p>
          
          <div className="flex flex-col sm:flex-row justify-center gap-4">
            <button 
              onClick={() => setChatOpen(true)}
              className="px-8 py-4 bg-white text-slate-900 font-bold rounded-lg hover:bg-slate-200 transition-colors shadow-lg shadow-white/5"
            >
              Ask about my Resume
            </button>
            <button 
              onClick={() => document.getElementById('work').scrollIntoView({behavior: 'smooth'})}
              className="px-8 py-4 bg-slate-900 text-white font-semibold rounded-lg border border-slate-700 hover:border-sky-500/50 transition-colors"
            >
              View Track Record
            </button>
          </div>
        </div>
      </section>

      {/* Product Philosophy */}
      <section className="py-24 bg-slate-900/50 border-y border-slate-800/50">
        <div className="max-w-6xl mx-auto px-6">
          <div className="mb-16">
            <h2 className="text-3xl font-bold text-white mb-4">Leadership Principles</h2>
            <p className="text-slate-400 max-w-4xl text-lg">
              I build platforms that accelerate engineering velocity and deliver measurable business impact. My focus is responsible AI, lovable developer experiences, and turning enterprise data into products that unlock revenue, efficiency, and customer satisfaction.
            </p>
          </div>

          <div className="grid md:grid-cols-3 gap-8">
            {DATA.philosophy.map((p) => (
              <div key={p.id} className="p-8 bg-slate-950 border border-slate-800 rounded-2xl hover:border-sky-500/30 transition-all hover:shadow-2xl hover:shadow-sky-900/10 group">
                <div className="w-14 h-14 bg-slate-900 rounded-xl flex items-center justify-center text-sky-500 mb-6 group-hover:scale-110 transition-transform border border-slate-800">
                  {p.icon}
                </div>
                <h3 className="text-xl font-bold mb-3 text-white">{p.title}</h3>
                <p className="text-slate-400 leading-relaxed font-light">{p.detail}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Experience & Impact */}
      <section id="work" className="py-24 px-6">
        <div className="max-w-4xl mx-auto">
          <h2 className="text-3xl font-bold mb-16 flex items-center gap-3 text-white">
            <BarChart className="text-sky-500" /> Impact History
          </h2>
          
          <div className="space-y-8 mb-24 relative before:absolute before:left-0 before:top-4 before:bottom-4 before:w-px before:bg-slate-800 md:before:left-[-2rem]">
            {DATA.experience.map((job) => (
              <div key={job.id} className="relative">
                {/* Timeline Dot */}
                <div className="hidden md:block absolute left-[-2.35rem] top-6 w-3 h-3 rounded-full bg-slate-950 border-2 border-sky-500 z-10"></div>
                
                <div className="p-8 bg-slate-900/30 border border-slate-800 rounded-xl hover:bg-slate-900 hover:border-sky-500/30 transition-all group hover:shadow-xl hover:shadow-sky-900/10">
                  <div className="flex flex-col md:flex-row md:items-center justify-between mb-4 gap-2">
                    <div>
                      <h3 className="text-2xl font-bold text-white group-hover:text-sky-400 transition-colors">{job.role}</h3>
                      <p className="text-slate-400 font-medium">{job.company}</p>
                    </div>
                    <span className="text-slate-500 font-mono text-sm bg-slate-900 px-3 py-1 rounded-md border border-slate-800">{job.year}</span>
                  </div>
                  
                  <div className="flex items-start gap-3 mt-6">
                    <ChevronRight className="text-sky-500 mt-1 shrink-0" size={18} />
                    <p className="text-slate-300 leading-relaxed">
                      <span className="font-semibold text-sky-100">Key Outcome:</span> {job.impact}
                    </p>
                  </div>
                </div>
              </div>
            ))}
          </div>

          {/* PLATFORM VALUE MULTIPLIER */}
          <PlatformValueMultiplier />

          {/* AI Generator Section */}
          <PitchGenerator />
          
        </div>
      </section>

      {/* Simple Footer */}
      <footer className="py-12 border-t border-slate-900 text-center text-slate-500">
        <div className="max-w-6xl mx-auto px-6 flex flex-col md:flex-row justify-between items-center gap-4">
          <p>© {new Date().getFullYear()} Steven L. Washington.</p>
          <div className="flex gap-6 text-sm font-medium">
            <button onClick={() => setChatOpen(true)} className="hover:text-white transition-colors">Contact via AI</button>
            <a href={DATA.profile.social.linkedin} className="hover:text-white transition-colors">LinkedIn</a>
          </div>
        </div>
      </footer>

      {/* The Chat Application and Contact Modal */}
      <ChatWidget 
        isOpen={chatOpen} 
        toggleChat={() => setChatOpen(!chatOpen)} 
      />

    </div>
  );
};

export default App;
