# AI_HB_Questionnaire

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AI Security Capability Questionnaire</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,sans-serif;color:#1a1a1a;background:#f5f5f2;padding:2rem 1rem}
.wrap{max-width:960px;margin:0 auto}
.header{margin-bottom:1.5rem}
.header h1{font-size:22px;font-weight:500;margin-bottom:4px}
.header p{font-size:13px;color:#666}
.tabs{display:flex;gap:4px;flex-wrap:wrap;margin-bottom:1.5rem;border-bottom:1px solid #ddd;padding-bottom:8px}
.tab{font-size:12px;padding:5px 10px;border:1px solid #ccc;border-radius:8px;cursor:pointer;background:transparent;color:#555;transition:all .15s;white-space:nowrap}
.tab:hover{background:#eee}
.tab.active{background:#e8e8e4;color:#1a1a1a;border-color:#999}
.section{display:none}
.section.active{display:block}
.section-header{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:1rem;gap:12px}
.section-title{font-size:16px;font-weight:500}
.section-meta{font-size:12px;color:#666;margin-top:2px}
.priority-badge{font-size:11px;padding:3px 8px;border-radius:8px;white-space:nowrap;flex-shrink:0}
.p-primary{background:#E1F5EE;color:#085041}
.p-secondary{background:#E6F1FB;color:#0C447C}
.p-tertiary{background:#F1EFE8;color:#444}
.q-group{margin-bottom:1.5rem;background:#fff;border:1px solid #e0e0db;border-radius:12px;padding:1rem 1.25rem}
.q-group-label{font-size:11px;font-weight:500;color:#888;margin-bottom:10px;text-transform:uppercase;letter-spacing:.04em}
.q-row{display:grid;grid-template-columns:1fr auto;gap:12px;align-items:start;padding:10px 0;border-bottom:1px solid #f0f0ec}
.q-row:last-child{border-bottom:none}
.q-text{font-size:13px;line-height:1.5}
.q-sub{font-size:12px;color:#888;margin-top:3px}
.q-controls{display:flex;align-items:center;gap:6px;flex-shrink:0}
select{font-size:12px;padding:4px 8px;border:1px solid #ccc;border-radius:8px;background:#fff;color:#1a1a1a;cursor:pointer;min-width:130px}
select:focus{outline:none;border-color:#888}
.note-input{font-size:12px;padding:4px 8px;border:1px solid #ccc;border-radius:8px;background:#fff;color:#1a1a1a;width:150px}
.note-input:focus{outline:none;border-color:#888}
.score-bar{position:sticky;top:0;z-index:10;background:#f5f5f2;border-bottom:1px solid #ddd;padding:10px 0;margin-bottom:1rem;display:grid;grid-template-columns:repeat(auto-fit,minmax(110px,1fr));gap:8px}
.score-card{background:#fff;border:1px solid #e0e0db;border-radius:8px;padding:8px 12px;text-align:center}
.score-card .sc-label{font-size:11px;color:#888}
.score-card .sc-val{font-size:18px;font-weight:500}
.actions{margin-top:1.5rem;display:flex;justify-content:flex-end;gap:8px}
.btn{font-size:13px;padding:7px 16px;border:1px solid #ccc;border-radius:8px;cursor:pointer;background:#fff;color:#1a1a1a}
.btn:hover{background:#eee}
.btn.primary{background:#1a1a1a;color:#fff;border-color:#1a1a1a}
.btn.primary:hover{background:#333}
.legend{display:flex;gap:12px;flex-wrap:wrap;margin-bottom:1rem}
.leg-item{display:flex;align-items:center;gap:5px;font-size:11px;color:#666}
.leg-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
@media(max-width:600px){
  .q-row{grid-template-columns:1fr}
  .q-controls{flex-wrap:wrap}
  .note-input{width:100%}
  select{min-width:100%}
}
</style>
</head>
<body>
<div class="wrap">
  <div class="header">
    <h1>AI security capability questionnaire</h1>
    <p>Score each capability: Full / Partial / Roadmap / Not supported. Use notes for vendor-specific detail.</p>
  </div>

  <div class="score-bar" id="scoreBar"></div>

  <div class="legend">
    <span class="leg-item"><span class="leg-dot" style="background:#1D9E75"></span>Primary priority</span>
    <span class="leg-item"><span class="leg-dot" style="background:#378ADD"></span>Secondary priority</span>
    <span class="leg-item"><span class="leg-dot" style="background:#888"></span>Tertiary</span>
  </div>

  <div class="tabs" id="tabBar"></div>
  <div id="sections"></div>

  <div class="actions">
    <button class="btn" onclick="resetAll()">Reset</button>
    <button class="btn primary" onclick="exportCSV()">Export CSV</button>
  </div>
</div>

<script>
const DATA = [
{id:"runtime",label:"Runtime security",priority:"primary",vendors:"Lasso, Troj",meta:"AI firewall — highest priority capability",groups:[
  {label:"Deployment modes",qs:[
    {q:"API-based integration (out-of-band)",sub:"REST/webhook interception without inline traffic"},
    {q:"Inline / reverse proxy deployment",sub:"Full traffic interception with block capability"},
    {q:"Forward proxy / gateway mode",sub:"Explicit proxy for HTTP/S traffic"},
    {q:"Browser extension deployment",sub:"Chrome/Edge/Firefox — user-level enforcement"},
    {q:"SDK / library integration",sub:"In-app instrumentation for LLM calls"},
    {q:"Endpoint agent deployment",sub:"OS-level agent on managed devices"},
    {q:"AI gateway integration",sub:"Native plugin for AWS AI Gateway, Azure APIM, Kong, etc."},
    {q:"On-premises deployment option",sub:"Air-gapped or private cloud"},
    {q:"SaaS / cloud-hosted option"},
    {q:"Hybrid deployment support",sub:"Mix of on-prem + cloud enforcement points"},
  ]},
  {label:"Threat detection",qs:[
    {q:"Direct prompt injection detection",sub:"Malicious instructions in user input"},
    {q:"Indirect prompt injection detection",sub:"Injections via retrieved documents, tools, web content"},
    {q:"Jailbreak detection",sub:"Role-play, DAN, encoding-based bypass attempts"},
    {q:"Multi-modal support",sub:"Image, audio, video inputs to LLMs"},
    {q:"Toxic / harmful content detection"},
    {q:"OWASP LLM Top 10 coverage",sub:"State which items are covered"},
    {q:"Agentic task drift detection",sub:"Agent deviates from intended scope or plan"},
    {q:"Data poisoning detection",sub:"Malicious content in training or RAG pipelines"},
    {q:"Model inversion / extraction detection"},
  ]},
  {label:"Data loss prevention",qs:[
    {q:"Sensitive data detection in prompts",sub:"PII, PHI, credentials, financial data"},
    {q:"File upload scanning",sub:"Docs, images, spreadsheets uploaded to AI apps"},
    {q:"Clipboard / copy-paste interception",sub:"Data pasted into AI chat interfaces"},
    {q:"Full file content scanning",sub:"Not just metadata — actual file body"},
    {q:"Code secrets / credential detection",sub:"API keys, tokens, passwords in code snippets"},
    {q:"Sensitivity label / classification tag enforcement",sub:"Block based on MIP/AIP labels"},
    {q:"Custom content moderation rules",sub:"E.g. block resume uploads, legal docs, IP"},
    {q:"Prohibited topics / profanity filtering"},
    {q:"Dictionary / regex pattern matching"},
    {q:"LLM-based semantic analysis",sub:"Beyond regex — contextual understanding"},
    {q:"Intent analysis",sub:"Inferring purpose behind ambiguous queries"},
  ]},
  {label:"Response & enforcement",qs:[
    {q:"Block mode support",sub:"Hard block with user-facing message"},
    {q:"Monitor-only mode",sub:"Log and alert without blocking"},
    {q:"Model or app redirect based on intent",sub:"Route to safer model or approved app"},
    {q:"User notification / awareness messaging",sub:"Customizable coaching messages"},
    {q:"Per-policy block vs monitor granularity",sub:"Different actions per rule"},
    {q:"Response scanning (not just input)",sub:"Detect issues in LLM output before delivery"},
  ]},
  {label:"Network & infrastructure",qs:[
    {q:"Network-level interception (MITM/TLS inspection)"},
    {q:"API-level interception (no network tap needed)"},
    {q:"Incognito / private browsing support"},
    {q:"Mobile device support",sub:"iOS and Android"},
    {q:"MDM integration",sub:"Jamf, Intune, etc."},
  ]},
]},

{id:"discovery",label:"Discovery & inventory",priority:"primary",vendors:"Palo Alto AIRS, Prisma AISPM",meta:"AI app, model, agent, and API discovery",groups:[
  {label:"Application discovery",qs:[
    {q:"SaaS AI app discovery",sub:"Detect ChatGPT, Copilot, Gemini, Perplexity, etc. in use"},
    {q:"Number of AI apps in discovery catalog",sub:"How many apps identified out-of-box"},
    {q:"Shadow AI detection",sub:"Unsanctioned AI tools in use"},
    {q:"App categorization and risk scoring"},
    {q:"App data access mapping",sub:"What data flows to which AI apps"},
    {q:"Browser-based discovery",sub:"Via browser extension or proxy"},
    {q:"Network-based discovery",sub:"Via firewall or proxy logs"},
  ]},
  {label:"Model inventory",qs:[
    {q:"Model discovery — cloud-hosted models",sub:"OpenAI, Anthropic, Google, Cohere, etc."},
    {q:"Model discovery — self-hosted / on-prem models",sub:"Llama, Mistral, Falcon running locally"},
    {q:"Model versioning and lifecycle tracking",sub:"Track model updates, deprecations"},
    {q:"Model metadata capture",sub:"Provider, version, capabilities, risk tier"},
  ]},
  {label:"Agent & plugin discovery",qs:[
    {q:"Agentic AI discovery — SaaS platforms",sub:"ServiceNow AI agents, Salesforce Agentforce, SAP Joule"},
    {q:"Agentic AI discovery — Microsoft ecosystem",sub:"Copilot Studio, M365 Copilot agents, Azure AI Foundry"},
    {q:"Agentic AI discovery — Cloud builder platforms",sub:"AWS Bedrock agents, Amazon Q, Google Vertex AI agents"},
    {q:"Agentic AI discovery — Claude / Anthropic",sub:"Claude.ai, Claude Cowork, API-built agents"},
    {q:"Agentic AI discovery — workstation / local",sub:"Local agent processes, MCP servers, tool configs"},
    {q:"Code assistant discovery",sub:"GitHub Copilot, Cursor, Tabnine, Codeium, Continue, etc."},
    {q:"Plugin / tool discovery",sub:"Plugins attached to agents: web search, code exec, etc."},
    {q:"API endpoint discovery",sub:"LLM API calls made from apps or agents"},
    {q:"MCP server discovery",sub:"Model Context Protocol servers in use"},
  ]},
  {label:"Access & entitlement mapping",qs:[
    {q:"App access mapping",sub:"Who has access to which AI apps"},
    {q:"Agentic data access mapping",sub:"What data/APIs can agents reach"},
    {q:"Agentic permission / entitlement mapping",sub:"OAuth scopes, service account privileges"},
    {q:"Identity-to-AI-usage correlation",sub:"Link user identities to AI activity"},
  ]},
]},

{id:"agentic",label:"Agentic security",priority:"primary",vendors:"Zenity, Straikers, Palo Alto, Lasso",meta:"Security for autonomous AI agents",groups:[
  {label:"Agentic visibility",qs:[
    {q:"Agent action monitoring",sub:"Log all tool calls, API calls, decisions made by agents"},
    {q:"Agent workflow / chain visibility",sub:"Visualize multi-step agent execution"},
    {q:"Agent identity tracking",sub:"Distinguish human vs agent actions in logs"},
    {q:"Tool / plugin usage tracking",sub:"Which tools agents invoke and with what inputs"},
    {q:"Inter-agent communication monitoring",sub:"Agent-to-agent calls in multi-agent systems"},
  ]},
  {label:"Agentic threat detection",qs:[
    {q:"Agentic task drift detection",sub:"Agent pursuing goals outside defined scope"},
    {q:"Privilege escalation detection",sub:"Agent acquiring permissions it shouldn't have"},
    {q:"Unauthorized data exfiltration by agents"},
    {q:"Agent impersonation detection",sub:"Agent acting as another identity"},
    {q:"Prompt injection via tool results",sub:"Injected instructions returned from web/APIs/docs"},
    {q:"Agentic UEBA / behavioral baseline",sub:"Detect anomalous agent behavior vs baseline"},
  ]},
  {label:"Agentic identity & config (AI-SPM overlap)",qs:[
    {q:"Service account / non-human identity discovery",sub:"Enumerate AI-related service accounts and API keys"},
    {q:"Agentic identity misconfiguration detection",sub:"Overly permissive scopes, unused credentials"},
    {q:"Secret exposure detection",sub:"API keys/tokens in agent configs, prompts, repos"},
    {q:"System prompt exposure detection",sub:"Leaked or accessible system prompts"},
    {q:"Agent configuration drift detection",sub:"Changes to agent behavior or tool access"},
  ]},
  {label:"Agentic enforcement",qs:[
    {q:"Agent action blocking / policy enforcement",sub:"Prevent specific agent actions in real time"},
    {q:"Human-in-the-loop controls",sub:"Require approval for high-risk agent actions"},
    {q:"Agent sandboxing / isolation support",sub:"Contain agent blast radius"},
  ]},
]},

{id:"employee",label:"Employee AI access",priority:"secondary",vendors:"Palo Alto, Witness.ai, Prompt Security",meta:"Governing employee use of AI tools",groups:[
  {label:"Policy & access governance",qs:[
    {q:"Per-user or per-group AI app access policies"},
    {q:"Allowlist / blocklist for AI applications"},
    {q:"Business justification workflows",sub:"Users request access with approval flow"},
    {q:"Time-of-day or location-based access controls"},
    {q:"Role-based AI entitlements",sub:"Different access tiers by job function"},
  ]},
  {label:"Behavioral monitoring",qs:[
    {q:"User AI usage dashboards",sub:"Individual and aggregate usage patterns"},
    {q:"Unusual usage pattern alerting",sub:"Spike in volume, new apps, off-hours use"},
    {q:"User risk scoring based on AI behavior"},
    {q:"Coaching / nudge messages for policy violations",sub:"Not just block — educate the user"},
  ]},
  {label:"Code assistant controls",qs:[
    {q:"Code assistant DLP",sub:"Block secrets, PII, IP in code sent to AI"},
    {q:"Code suggestion monitoring",sub:"Track what code is accepted from AI"},
    {q:"IDE plugin for code assistant controls",sub:"VS Code, JetBrains, etc."},
    {q:"Code assistant allowlist / blocklist by tool"},
  ]},
]},

{id:"modelscan",label:"Model scanning",priority:"secondary",vendors:"HiddenLayer",meta:"Supply chain and model integrity",groups:[
  {label:"Model security scanning",qs:[
    {q:"Static model file scanning",sub:"Scan .pkl, .pt, .safetensors, GGUF, etc. for malicious payloads"},
    {q:"Deserialization attack detection",sub:"Pickle exploits, arbitrary code in model files"},
    {q:"Embedded malware / backdoor detection"},
    {q:"Model weight integrity verification",sub:"Detect tampering vs known-good hash"},
    {q:"Model registry scanning",sub:"Hugging Face, GitHub, internal registries"},
  ]},
  {label:"AI-SBOM & supply chain",qs:[
    {q:"AI Software Bill of Materials generation",sub:"Model provenance, dependencies, training data sources"},
    {q:"Third-party model dependency tracking"},
    {q:"Model fine-tune lineage tracking",sub:"Base model + fine-tune chain"},
    {q:"Training data poisoning indicators"},
    {q:"CI/CD pipeline integration for model scanning"},
  ]},
]},

{id:"aispm",label:"AI-SPM",priority:"secondary",vendors:"Wiz, Palo Alto AISPM",meta:"AI Security Posture Management",groups:[
  {label:"AI asset posture",qs:[
    {q:"Cloud AI service discovery",sub:"AWS Bedrock, Azure OpenAI, Vertex — what's deployed"},
    {q:"AI workload misconfiguration detection",sub:"Public exposure, weak auth, unencrypted endpoints"},
    {q:"AI data store exposure",sub:"S3/blob/vector DBs accessible to AI workloads"},
    {q:"LLM application code scanning",sub:"SAST for LLM-specific vulnerabilities"},
    {q:"AI pipeline security assessment",sub:"Training, fine-tuning, inference pipelines"},
  ]},
  {label:"Identity & entitlements",qs:[
    {q:"AI service account enumeration and review"},
    {q:"Excessive permission detection for AI workloads"},
    {q:"Cross-account / cross-tenant AI access risk"},
    {q:"API key rotation enforcement / monitoring"},
  ]},
  {label:"Continuous posture monitoring",qs:[
    {q:"Posture score / risk dashboard"},
    {q:"Drift detection from baseline",sub:"Alert on new AI resources or permission changes"},
    {q:"Remediation guidance",sub:"Step-by-step fix instructions per finding"},
    {q:"Integration with cloud security graph",sub:"Correlate AI risk with broader cloud context"},
  ]},
]},

{id:"redteam",label:"Red teaming",priority:"secondary",vendors:"Troj, Lasso",meta:"Adversarial testing of AI systems",groups:[
  {label:"Attack simulation",qs:[
    {q:"Automated adversarial prompt generation"},
    {q:"Jailbreak attempt library",sub:"Coverage of known and novel jailbreak techniques"},
    {q:"Indirect prompt injection simulation",sub:"Inject via RAG docs, tool results, emails"},
    {q:"Multi-turn attack simulation",sub:"Attacks that unfold over conversation history"},
    {q:"Multi-modal attack simulation",sub:"Image/audio-based attacks"},
    {q:"Agentic attack simulation",sub:"Test agent manipulation, goal hijacking"},
  ]},
  {label:"Coverage & reporting",qs:[
    {q:"OWASP LLM Top 10 test coverage"},
    {q:"MITRE ATLAS technique coverage"},
    {q:"Custom attack scenario definition"},
    {q:"Continuous / scheduled testing",sub:"Not just one-time assessments"},
    {q:"Findings integration with issue trackers",sub:"Jira, ServiceNow, etc."},
    {q:"Executive and technical reporting"},
  ]},
]},

{id:"tprm",label:"AI TPRM",priority:"secondary",vendors:"Credo AI, Varonis Atlas",meta:"Third-party AI risk management",groups:[
  {label:"Vendor assessment",qs:[
    {q:"AI vendor risk questionnaire library",sub:"Pre-built questionnaires for AI providers"},
    {q:"Automated vendor assessment workflows"},
    {q:"Continuous vendor monitoring",sub:"Alert on vendor policy / model changes"},
    {q:"Data residency and processing verification"},
    {q:"Subprocessor chain visibility"},
  ]},
  {label:"Contract & policy",qs:[
    {q:"AI-specific contract clause library",sub:"Data use, retention, opt-out provisions"},
    {q:"Terms of service change monitoring",sub:"Alert when AI vendor ToS updates"},
    {q:"Data deletion verification workflow"},
  ]},
]},

{id:"compliance",label:"Compliance",priority:"tertiary",vendors:"Credo AI, Varonis Atlas",meta:"Regulatory and framework mapping",groups:[
  {label:"Framework coverage",qs:[
    {q:"OWASP LLM Top 10 mapping"},
    {q:"NIST AI RMF mapping"},
    {q:"EU AI Act mapping",sub:"Risk tier classification, Article coverage"},
    {q:"ISO/IEC 42001 mapping",sub:"AI management system standard"},
    {q:"SOC 2 AI addendum mapping"},
    {q:"HIPAA / GDPR AI processing guidance"},
    {q:"Custom framework / internal policy mapping"},
  ]},
  {label:"Evidence & audit",qs:[
    {q:"Automated compliance evidence collection"},
    {q:"Audit-ready reporting export",sub:"PDF, XLSX reports for auditors"},
    {q:"SIEM integration for AI event logging",sub:"Splunk, Sentinel, Chronicle, etc."},
    {q:"Immutable audit log support"},
    {q:"Policy exception management and tracking"},
    {q:"Risk register integration"},
  ]},
]},

{id:"integrations",label:"Integrations",priority:"tertiary",vendors:"All vendors",meta:"Ecosystem and platform integrations",groups:[
  {label:"Cloud & AI platform integrations",qs:[
    {q:"AWS native integration",sub:"Bedrock, GuardDuty, Security Hub"},
    {q:"Azure native integration",sub:"Azure OpenAI, Defender, Sentinel"},
    {q:"GCP native integration",sub:"Vertex AI, Security Command Center"},
    {q:"AI gateway integration",sub:"Kong, Apigee, MuleSoft, AWS AI Gateway"},
    {q:"Model hub integration",sub:"Hugging Face, Azure ML, SageMaker"},
  ]},
  {label:"Security stack integrations",qs:[
    {q:"SIEM integration",sub:"Splunk, Sentinel, Chronicle, QRadar"},
    {q:"SOAR integration",sub:"Palo Cortex XSOAR, Splunk SOAR, etc."},
    {q:"CASB integration"},
    {q:"SSO / IdP integration",sub:"Okta, Entra ID, Ping"},
    {q:"DLP platform integration",sub:"Microsoft Purview, Symantec DLP, etc."},
    {q:"Ticketing / ITSM integration",sub:"Jira, ServiceNow"},
    {q:"REST API / webhooks for custom integration"},
  ]},
]},
];

const OPTIONS=["Full","Partial","Roadmap","Not supported"];
let state={};
DATA.forEach(s=>s.groups.forEach(g=>g.qs.forEach((q,i)=>{
  const key=s.id+"__"+g.label+"__"+i;
  state[key]={val:"",note:""};
})));

function buildTabs(){
  const bar=document.getElementById("tabBar");
  DATA.forEach((s,i)=>{
    const b=document.createElement("button");
    b.className="tab"+(i===0?" active":"");
    b.textContent=s.label;
    b.onclick=()=>{
      document.querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
      b.classList.add("active");
      document.querySelectorAll(".section").forEach(t=>t.classList.remove("active"));
      document.getElementById("sec_"+s.id).classList.add("active");
    };
    bar.appendChild(b);
  });
}

function buildSections(){
  const cont=document.getElementById("sections");
  DATA.forEach((s,si)=>{
    const div=document.createElement("div");
    div.className="section"+(si===0?" active":"");
    div.id="sec_"+s.id;
    const pClass=s.priority==="primary"?"p-primary":s.priority==="secondary"?"p-secondary":"p-tertiary";
    div.innerHTML=`<div class="section-header"><div><div class="section-title">${s.label}</div><div class="section-meta">${s.meta} &nbsp;·&nbsp; <em>${s.vendors}</em></div></div><span class="priority-badge ${pClass}">${s.priority}</span></div>`;
    s.groups.forEach(g=>{
      const gd=document.createElement("div");
      gd.className="q-group";
      gd.innerHTML=`<div class="q-group-label">${g.label}</div>`;
      g.qs.forEach((q,i)=>{
        const key=s.id+"__"+g.label+"__"+i;
        const row=document.createElement("div");
        row.className="q-row";
        row.innerHTML=`<div><div class="q-text">${q.q}</div>${q.sub?`<div class="q-sub">${q.sub}</div>`:""}</div><div class="q-controls"><select data-key="${key}"><option value="">— select —</option>${OPTIONS.map(o=>`<option value="${o}">${o}</option>`).join("")}</select><input class="note-input" data-key-note="${key}" placeholder="Notes…" /></div>`;
        gd.appendChild(row);
      });
      div.appendChild(gd);
    });
    cont.appendChild(div);
  });

  document.querySelectorAll("select[data-key]").forEach(el=>{
    el.addEventListener("change",e=>{
      state[e.target.dataset.key].val=e.target.value;
      updateScores();
    });
  });
  document.querySelectorAll("input[data-key-note]").forEach(el=>{
    el.addEventListener("input",e=>{
      state[e.target.dataset.keyNote].note=e.target.value;
    });
  });
}

function updateScores(){
  const bar=document.getElementById("scoreBar");
  bar.innerHTML="";
  let totalFull=0,totalQ=0;
  DATA.forEach(s=>{
    let sf=0,sq=0;
    s.groups.forEach(g=>g.qs.forEach((q,i)=>{
      const key=s.id+"__"+g.label+"__"+i;
      const v=state[key].val;
      sq++;totalQ++;
      if(v==="Full"){sf++;totalFull++;}
    }));
    const pct=sq>0?Math.round((sf/sq)*100):0;
    const color=pct>=70?"#1D9E75":pct>=40?"#378ADD":"#E24B4A";
    const card=document.createElement("div");
    card.className="score-card";
    card.innerHTML=`<div class="sc-label">${s.label.length>16?s.label.slice(0,15)+"…":s.label}</div><div class="sc-val" style="color:${color}">${pct}%</div>`;
    bar.appendChild(card);
  });
  const overall=totalQ>0?Math.round((totalFull/totalQ)*100):0;
  const color=overall>=70?"#1D9E75":overall>=40?"#378ADD":"#E24B4A";
  const card=document.createElement("div");
  card.className="score-card";
  card.innerHTML=`<div class="sc-label">Overall (full)</div><div class="sc-val" style="font-size:20px;color:${color}">${overall}%</div>`;
  bar.appendChild(card);
}

function resetAll(){
  Object.keys(state).forEach(k=>{state[k]={val:"",note:""};});
  document.querySelectorAll("select[data-key]").forEach(el=>el.value="");
  document.querySelectorAll("input[data-key-note]").forEach(el=>el.value="");
  updateScores();
}

function exportCSV(){
  let rows=["Section,Priority,Group,Question,Sub-text,Response,Notes"];
  DATA.forEach(s=>{
    s.groups.forEach(g=>{
      g.qs.forEach((q,i)=>{
        const key=s.id+"__"+g.label+"__"+i;
        const v=state[key].val||"";
        const n=(state[key].note||"").replace(/"/g,"'");
        const sub=(q.sub||"").replace(/"/g,"'");
        rows.push(`"${s.label}","${s.priority}","${g.label}","${q.q}","${sub}","${v}","${n}"`);
      });
    });
  });
  const blob=new Blob([rows.join("\n")],{type:"text/csv"});
  const url=URL.createObjectURL(blob);
  const a=document.createElement("a");
  a.href=url;a.download="ai_security_questionnaire.csv";a.click();
  URL.revokeObjectURL(url);
}

buildTabs();
buildSections();
updateScores();
</script>
</body>
</html>
