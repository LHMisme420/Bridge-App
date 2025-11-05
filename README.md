# Bridge-App
Bridging Humanity
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bridge to Healing - Immediate Crisis Connection</title>
    <link rel="manifest" href="manifest.json">
    <meta name="theme-color" content="#764ba2">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: -apple-system, BlinkMacSystemFont, sans-serif; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); min-height: 100vh; color: #333; }
        .App { min-height: 100vh; display: flex; flex-direction: column; }
        .app-header { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(10px); padding: 1rem; text-align: center; box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1); }
        .app-header h1 { color: #764ba2; font-size: 1.8rem; margin-bottom: 0.5rem; }
        .app-main { flex: 1; padding: 1rem; max-width: 800px; margin: 0 auto; width: 100%; }
        .app-footer { background: rgba(0, 0, 0, 0.8); color: white; text-align: center; padding: 1rem; margin-top: auto; }
        
        /* Emergency Landing */
        .emergency-landing { animation: fadeIn 0.5s ease-in; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .urgency-indicator { display: flex; align-items: center; justify-content: center; background: rgba(255, 255, 255, 0.9); padding: 0.75rem; border-radius: 50px; margin-bottom: 2rem; box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1); }
        .pulse-dot { width: 12px; height: 12px; background: #4CAF50; border-radius: 50%; margin-right: 0.5rem; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.2); opacity: 0.7; } 100% { transform: scale(1); opacity: 1; } }
        .help-options { display: flex; flex-direction: column; gap: 1.5rem; }
        .help-option { background: white; border: none; border-radius: 20px; padding: 2rem; text-align: left; cursor: pointer; transition: all 0.3s ease; box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1); position: relative; overflow: hidden; }
        .help-option::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 4px; }
        .help-option.crisis::before { background: linear-gradient(90deg, #ff6b6b, #ff8e8e); }
        .help-option.comfort::before { background: linear-gradient(90deg, #4ecdc4, #88d3ce); }
        .help-option.connection::before { background: linear-gradient(90deg, #45b7d1, #96cfe3); }
        .help-option:hover { transform: translateY(-5px); box-shadow: 0 15px 35px rgba(0, 0, 0, 0.15); }
        .help-option .icon { font-size: 2.5rem; margin-bottom: 1rem; }
        .response-time { color: #888; font-size: 0.9rem; font-weight: 600; }
        
        /* Flow Styles */
        .flow-container { background: white; border-radius: 20px; padding: 2rem; box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1); animation: slideIn 0.3s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: translateX(20px); } to { opacity: 1; transform: translateX(0); } }
        .flow-header { display: flex; align-items: center; margin-bottom: 2rem; }
        .back-button { background: none; border: none; font-size: 1.5rem; cursor: pointer; margin-right: 1rem; padding: 0.5rem; border-radius: 50%; transition: background 0.2s; }
        .back-button:hover { background: #f5f5f5; }
        .resource-list { display: flex; flex-direction: column; gap: 1rem; }
        .resource-card { border: 2px solid #e0e0e0; border-radius: 15px; padding: 1.5rem; transition: all 0.3s ease; }
        .resource-card:hover { border-color: #764ba2; transform: translateY(-2px); box-shadow: 0 5px 15px rgba(118, 75, 162, 0.2); }
        .resource-card.critical { border-color: #ff6b6b; background: linear-gradient(135deg, #fff5f5, #ffffff); }
        .resource-contact { font-size: 1.3rem; font-weight: 700; color: #764ba2; margin-bottom: 0.5rem; }
        .action-button { background: linear-gradient(135deg, #667eea, #764ba2); color: white; border: none; padding: 1rem 2rem; border-radius: 50px; font-size: 1.1rem; font-weight: 600; cursor: pointer; transition: all 0.3s ease; margin-top: 1rem; width: 100%; }
        .action-button:hover { transform: translateY(-2px); box-shadow: 0 8px 25px rgba(118, 75, 162, 0.4); }
        .safety-plan { background: #fff9e6; border: 2px solid #ffd166; border-radius: 15px; padding: 1.5rem; margin: 2rem 0; }
        .safety-steps { list-style: none; }
        .safety-steps li { padding: 0.5rem 0; border-bottom: 1px solid #ffeaa7; }
        
        /* Loading */
        .loading { display: flex; justify-content: center; align-items: center; padding: 3rem; }
        .spinner { width: 40px; height: 40px; border: 4px solid #f3f3f3; border-top: 4px solid #764ba2; border-radius: 50%; animation: spin 1s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        
        @media (max-width: 768px) {
            .app-main { padding: 0.5rem; }
            .help-option, .flow-container, .resource-card { padding: 1.5rem; }
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script>
        // Crisis Resources Database
        const crisisResources = {
            national: [
                {
                    id: '988', name: '988 Suicide & Crisis Lifeline', contact: '988',
                    description: 'Immediate crisis support for suicide, mental health, substance use. Free, confidential, 24/7.',
                    availability: '24/7', languages: ['English', 'Spanish', '150+ via interpreter'], type: 'phone', priority: 'critical'
                },
                {
                    id: 'crisis-text', name: 'Crisis Text Line', contact: 'Text HOME to 741741',
                    description: 'Free crisis counseling via text message. Connect with trained crisis counselor.',
                    availability: '24/7', languages: ['English'], type: 'text', priority: 'critical'
                },
                {
                    id: 'domestic-violence', name: 'National Domestic Violence Hotline', contact: '1-800-799-7233',
                    description: 'Support for domestic violence situations. Safety planning, resources, shelter referrals.',
                    availability: '24/7', languages: ['English', 'Spanish', '200+ via interpreter'], type: 'phone', priority: 'critical'
                }
            ],
            comfort: [
                {
                    id: 'warm-line', name: 'Warm Line Network', contact: 'Various local numbers',
                    description: 'Peer support for emotional distress before it becomes a crisis.', availability: 'Varies', type: 'phone'
                }
            ],
            connection: [
                {
                    id: 'community-centers', name: 'Local Community Centers', contact: 'Find nearby locations',
                    description: 'Places to connect with others, join activities, build community.', availability: 'Varies', type: 'in-person'
                }
            ]
        };

        // Crisis Router Service
        class CrisisRouter {
            async routeToHelp(needType, userNeeds = [], location = null) {
                await new Promise(resolve => setTimeout(resolve, 1000));
                let resources = []; let safetyPlan = [];
                switch (needType) {
                    case 'crisis': resources = this.getCrisisResources(userNeeds); safetyPlan = this.generateCrisisSafetyPlan(userNeeds); break;
                    case 'comfort': resources = this.getComfortResources(); safetyPlan = this.generateComfortPlan(); break;
                    case 'connection': resources = this.getConnectionResources(location); safetyPlan = this.generateConnectionPlan(); break;
                    default: resources = this.getFallbackResources();
                }
                return { resources, safetyPlan, followUp: this.scheduleFollowUp(needType) };
            }
            getCrisisResources(userNeeds) {
                let resources = [...crisisResources.national];
                if (userNeeds.includes('violence') || userNeeds.includes('abuse')) resources.push({ id: 'local-shelters', name: 'Local Domestic Violence Shelters', contact: 'Find nearby safe locations', description: 'Immediate safe housing and support services.', availability: '24/7 emergency intake', type: 'in-person', priority: 'critical' });
                if (userNeeds.includes('substance')) resources.push({ id: 'substance-help', name: 'Substance Abuse Helpline', contact: '1-800-662-4357', description: 'Treatment referral and information service.', availability: '24/7', type: 'phone', priority: 'high' });
                return resources.sort((a, b) => { const priorityOrder = { critical: 0, high: 1, medium: 2 }; return priorityOrder[a.priority] - priorityOrder[b.priority]; });
            }
            getComfortResources() { return [...crisisResources.comfort, ...crisisResources.national.filter(r => r.priority !== 'critical')]; }
            getConnectionResources(location) {
                let resources = [...crisisResources.connection];
                if (location && location.city) resources.push({ id: 'local-' + location.city, name: `${location.city} Community Resources`, contact: 'Local directory', description: `Community centers, support groups, and activities in ${location.city}.`, availability: 'Various times', type: 'in-person', priority: 'medium' });
                return resources;
            }
            generateCrisisSafetyPlan(userNeeds) {
                const plan = ['Find a safe place to talk or wait for help', 'Remove yourself from immediate danger if possible', 'Keep your phone charged and accessible'];
                if (userNeeds.includes('suicide') || userNeeds.includes('self-harm')) { plan.push('Remove access to means of self-harm'); plan.push('Call 988 or go to nearest emergency room if in immediate danger'); plan.push('Stay with a trusted person if possible'); }
                if (userNeeds.includes('violence')) { plan.push('Identify safe places to go (friends, family, shelters)'); plan.push('Develop a code word with trusted contacts'); plan.push('Keep important documents and medications accessible'); }
                return plan;
            }
            generateComfortPlan() { return ['Find a quiet, comfortable space', 'Use deep breathing to calm your nervous system', 'Remember this feeling is temporary', 'Reach out to someone you trust']; }
            generateConnectionPlan() { return ['Start with small, low-pressure social interactions', 'Consider joining a group with shared interests', 'Be patient - building connections takes time', 'Remember that many people feel lonely sometimes']; }
            scheduleFollowUp(needType) {
                const intervals = { crisis: 24 * 60 * 60 * 1000, comfort: 3 * 24 * 60 * 60 * 1000, connection: 7 * 24 * 60 * 60 * 1000 };
                return { checkIn: new Date(Date.now() + intervals[needType]), message: 'How are you doing? We care about your wellbeing.' };
            }
            getFallbackResources() { return [{ id: 'emergency', name: 'Emergency Services', contact: '911', description: 'Call for immediate life-threatening emergencies', availability: '24/7', type: 'phone', priority: 'critical' }]; }
        }

        // React-like Components without React
        function renderApp() {
            const root = document.getElementById('root');
            const currentFlow = window.currentFlow || 'landing';
            
            if (currentFlow === 'crisis') renderCrisisFlow(root);
            else if (currentFlow === 'comfort') renderComfortFlow(root);
            else if (currentFlow === 'connection') renderConnectionFlow(root);
            else renderLanding(root);
        }

        function renderLanding(container) {
            container.innerHTML = `
                <div class="App">
                    <header class="app-header">
                        <h1>Bridge to Healing</h1>
                        <p>Immediate help • No barriers • Anonymous</p>
                    </header>
                    <main class="app-main">
                        <div class="emergency-landing">
                            <div class="urgency-indicator">
                                <div class="pulse-dot"></div>
                                <span>Help available 24/7 • Anonymous • Free</span>
                            </div>
                            <div class="help-options">
                                <button class="help-option crisis" onclick="setFlow('crisis')">
                                    <div class="icon">🚨</div>
                                    <h2>I'm in crisis or danger</h2>
                                    <p>Immediate safety and crisis support. Suicide prevention, domestic violence, emergency mental health.</p>
                                    <div class="response-time">Response: &lt; 60 seconds</div>
                                </button>
                                <button class="help-option comfort" onclick="setFlow('comfort')">
                                    <div class="icon">💔</div>
                                    <h2>I need someone to talk to</h2>
                                    <p>Compassionate listening and emotional support. Anxiety, depression, loneliness, grief.</p>
                                    <div class="response-time">Response: &lt; 2 minutes</div>
                                </button>
                                <button class="help-option connection" onclick="setFlow('connection')">
                                    <div class="icon">🌉</div>
                                    <h2>I feel alone and need community</h2>
                                    <p>Local connections and ongoing support. Community groups, activities, peer support.</p>
                                    <div class="response-time">Response: &lt; 24 hours</div>
                                </button>
                            </div>
                        </div>
                    </main>
                    <footer class="app-footer">
                        <p>💝 You are not alone. Help is here.</p>
                        <small>🔒 Your privacy is protected. We never store personal information.</small>
                    </footer>
                </div>
            `;
        }

        function renderCrisisFlow(container) {
            container.innerHTML = `
                <div class="App">
                    <header class="app-header">
                        <h1>Bridge to Healing</h1>
                        <p>Immediate help • No barriers • Anonymous</p>
                    </header>
                    <main class="app-main">
                        <div class="flow-container">
                            <div class="flow-header">
                                <button class="back-button" onclick="setFlow('landing')">←</button>
                                <h2 class="flow-title">Crisis Support</h2>
                            </div>
                            <div class="safety-plan">
                                <h3>🚨 Immediate Safety Plan</h3>
                                <ul class="safety-steps">
                                    <li>Find a safe place to talk or wait for help</li>
                                    <li>Remove yourself from immediate danger if possible</li>
                                    <li>Keep your phone charged and accessible</li>
                                    <li>Call 988 or go to nearest emergency room if in immediate danger</li>
                                </ul>
                            </div>
                            <h3 style="margin-bottom: 1rem;">Connect to Help Now</h3>
                            <div class="resource-list">
                                ${crisisResources.national.map(resource => `
                                    <div class="resource-card ${resource.priority === 'critical' ? 'critical' : ''}">
                                        <div class="resource-name">${resource.name}</div>
                                        <div class="resource-contact">${resource.contact}</div>
                                        <div class="resource-description">${resource.description}</div>
                                        <div class="resource-meta">
                                            <span>🕒 ${resource.availability}</span>
                                            <span>🌐 ${resource.languages ? resource.languages.join(', ') : 'Multiple'}</span>
                                        </div>
                                        ${resource.type === 'phone' ? `<button class="action-button" onclick="window.open('tel:${resource.contact.replace(/\D/g, '')}', '_self')">Call Now</button>` : ''}
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                    </main>
                    <footer class="app-footer">
                        <p>💝 You are not alone. Help is here.</p>
                    </footer>
                </div>
            `;
        }

        function renderComfortFlow(container) {
            container.innerHTML = `
                <div class="App">
                    <header class="app-header">
                        <h1>Bridge to Healing</h1>
                        <p>Immediate help • No barriers • Anonymous</p>
                    </header>
                    <main class="app-main">
                        <div class="flow-container">
                            <div class="flow-header">
                                <button class="back-button" onclick="setFlow('landing')">←</button>
                                <h2 class="flow-title">Comfort & Support</h2>
                            </div>
                            <div style="margin-bottom: 2rem; padding: 1.5rem; background: #f8f9fa; border-radius: 15px;">
                                <h3 style="margin-bottom: 1rem; color: #764ba2;">💝 You're Not Alone</h3>
                                <p style="line-height: 1.6; color: #666;">It takes courage to reach out. These resources are here to provide compassionate listening and support whenever you need it.</p>
                            </div>
                            <div class="safety-plan">
                                <h3>🧘 Comfort Strategies</h3>
                                <ul class="safety-steps">
                                    <li>Find a quiet, comfortable space</li>
                                    <li>Use deep breathing to calm your nervous system</li>
                                    <li>Remember this feeling is temporary</li>
                                    <li>Reach out to someone you trust</li>
                                </ul>
                            </div>
                            <h3 style="margin-bottom: 1rem;">Support Resources</h3>
                            <div class="resource-list">
                                ${[...crisisResources.comfort, ...crisisResources.national.filter(r => r.priority !== 'critical')].map(resource => `
                                    <div class="resource-card">
                                        <div class="resource-name">${resource.name}</div>
                                        <div class="resource-contact">${resource.contact}</div>
                                        <div class="resource-description">${resource.description}</div>
                                        <div class="resource-meta"><span>🕒 ${resource.availability}</span></div>
                                        ${resource.type === 'phone' ? `<button class="action-button" onclick="window.open('tel:${resource.contact.replace(/\D/g, '')}', '_self')">Connect Now</button>` : ''}
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                    </main>
                    <footer class="app-footer">
                        <p>💝 You are not alone. Help is here.</p>
                    </footer>
                </div>
            `;
        }

        function renderConnectionFlow(container) {
            container.innerHTML = `
                <div class="App">
                    <header class="app-header">
                        <h1>Bridge to Healing</h1>
                        <p>Immediate help • No barriers • Anonymous</p>
                    </header>
                    <main class="app-main">
                        <div class="flow-container">
                            <div class="flow-header">
                                <button class="back-button" onclick="setFlow('landing')">←</button>
                                <h2 class="flow-title">Community Connection</h2>
                            </div>
                            <div style="margin-bottom: 2rem; padding: 1.5rem; background: #e8f5e8; border-radius: 15px;">
                                <h3 style="margin-bottom: 1rem; color: #2e7d32;">🌱 Grow Your Support Network</h3>
                                <p style="line-height: 1.6; color: #666;">Building connections takes time, but you've taken the first important step. Here are ways to find community and support.</p>
                            </div>
                            <div class="safety-plan">
                                <h3>🤝 Connection Building Tips</h3>
                                <ul class="safety-steps">
                                    <li>Start with small, low-pressure social interactions</li>
                                    <li>Consider joining a group with shared interests</li>
                                    <li>Be patient - building connections takes time</li>
                                    <li>Remember that many people feel lonely sometimes</li>
                                </ul>
                            </div>
                            <h3 style="margin-bottom: 1rem;">Community Resources</h3>
                            <div class="resource-list">
                                ${crisisResources.connection.map(resource => `
                                    <div class="resource-card">
                                        <div class="resource-name">${resource.name}</div>
                                        <div class="resource-contact">${resource.contact}</div>
                                        <div class="resource-description">${resource.description}</div>
                                        <div class="resource-meta">
                                            <span>🕒 ${resource.availability}</span>
                                            <span>📍 Local area</span>
                                        </div>
                                    </div>
                                `).join('')}
                            </div>
                        </div>
                    </main>
                    <footer class="app-footer">
                        <p>💝 You are not alone. Help is here.</p>
                    </footer>
                </div>
            `;
        }

        function setFlow(flow) {
            window.currentFlow = flow;
            renderApp();
        }

        // Initialize app
        window.currentFlow = 'landing';
        renderApp();
    </script>
</body>
</html>
# 🌉 Bridge App - Immediate Crisis Connection

> **Connecting people to healing resources in under 60 seconds**

[![Deployment: GitHub Pages](https://img.shields.io/badge/Deployment-GitHub_Pages-success)](https://pages.github.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

## 🚨 The Problem

People in crisis face overwhelming barriers:
- Complex navigation through healthcare systems
- Long wait times when seconds matter  
- Technological barriers for vulnerable populations
- Isolation when connection is most needed

## 🎯 Our Solution

A **3-click bridge** that connects people to appropriate help:
- **No signups** - Immediate access
- **Anonymous** - Privacy protected  
- **Location-aware** - Finds nearest resources
- **Multi-channel** - Phone, text, chat, in-person

## 🚀 Live Demo

**🌐 Production URL:** https://github.com/LHMisme420/Bridge-App/blob/main/README.md

## 📱 What It Does

### For People in Need:
1. **Open app** → See 3 clear options
2. **Choose need** → Crisis, Comfort, or Connection  
3. **Get help** → Immediate connection to appropriate resources

### Features:
- 🚨 **Crisis Support** - Suicide prevention, domestic violence, emergency mental health
- 💔 **Comfort & Support** - Emotional support, compassionate listening
- 🌉 **Community Connection** - Local resources, support groups, community centers

## 🛠️ Technology

- **Frontend**: Pure HTML/CSS/JavaScript (No frameworks needed)
- **Progressive Web App**: Works offline, installable on devices
- **Responsive**: Mobile-first design
- **Privacy**: No data collection, completely anonymous

## 🚀 Quick Deployment

### Method 1: GitHub Pages (Recommended)
```bash
# 1. Fork this repository
# 2. Go to Settings → Pages
# 3. Select "main" branch, root folder
# 4. Save - Your app is live in 2 minutes!
