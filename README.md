# Caffenio-HUB-Financiero
Aplicación Operaciones de Negocio Financiero
# En tu terminal local:
mkdir caffenio-ops && cd caffenio-ops
cp caffenio_ops_demo.html [caffenio_ops_demo_16.html](https://github.com/user-attachments/files/27376984/caffenio_ops_demo_16.html)    # ← renombrar a index.html
git init && git add . && git commit -m "Caffenio Ops v1.0"
gh repo create caffenio-ops --public --push
# Luego en GitHub → Settings → Pages → Branch: main → Save
# URL: https://rommelgil.github.io/caffenio-ops
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Caffenio Ops — SAP Automation Hub</title>
<!-- fonts: system stack -->
<style>
:root{
  --bg:#F0F2F5;--sidebar:#0F1724;--sidebar-hover:#1A2535;
  --orange:#F97316;--orange-d:#EA6B0A;
  --green:#22C55E;--green-bg:#DCFCE7;--green-tx:#15803D;
  --red:#EF4444;--red-bg:#FEE2E2;--red-tx:#B91C1C;
  --amber:#F59E0B;--amber-bg:#FEF3C7;--amber-tx:#92400E;
  --blue:#3B82F6;--blue-bg:#DBEAFE;--blue-tx:#1D4ED8;
  --teal:#14B8A6;--teal-bg:#CCFBF1;--teal-tx:#0F766E;
  --purple:#8B5CF6;--purple-bg:#EDE9FE;--purple-tx:#5B21B6;
  --card:#FFF;--border:#E5E7EB;--text:#111827;--sub:#6B7280;--light:#F9FAFB;
  --navy:#1E3A5F;--navy-dark:#0F2544;
  --obs-bg:#0D1117;--obs-card:#161B22;--obs-border:#21262D;--obs-text:#E6EDF3;--obs-sub:#8B949E;
  --font:-apple-system,BlinkMacSystemFont,'Segoe UI','Helvetica Neue',Arial,sans-serif;--mono:'SF Mono','Cascadia Code','Fira Code','Courier New',monospace;
  --sap-hdr-top:#E8EEF4;--sap-hdr-bot:#CDDCE9;--sap-border:#A0B8CC;--sap-navy:#003366;
}
*{margin:0;padding:0;box-sizing:border-box;}
body{font-family:var(--font);background:var(--bg);color:var(--text);display:flex;height:100vh;overflow:hidden;font-size:14px;}

/* ── SIDEBAR ── */
.sidebar{width:228px;min-width:228px;background:var(--sidebar);display:flex;flex-direction:column;height:100vh;user-select:none;}
.sidebar-logo{padding:18px 16px 16px;border-bottom:1px solid rgba(255,255,255,.07);}
.logo-wrap{display:flex;align-items:center;gap:10px;}
.logo-icon{width:36px;height:36px;background:var(--orange);border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:16px;font-weight:800;color:white;flex-shrink:0;}
.logo-main{font-size:14px;font-weight:700;color:white;}.logo-main span{color:var(--orange);}
.logo-sub{font-size:9px;font-weight:500;color:rgba(255,255,255,.35);letter-spacing:1px;text-transform:uppercase;}
.nav-section{padding:14px 12px 4px;font-size:9px;font-weight:700;color:rgba(255,255,255,.25);letter-spacing:1.2px;text-transform:uppercase;}
.nav-item{display:flex;align-items:center;gap:10px;padding:8px 12px;margin:1px 8px;border-radius:8px;cursor:pointer;font-size:12.5px;font-weight:500;color:rgba(255,255,255,.55);transition:all .15s;position:relative;}
.nav-item:hover{background:var(--sidebar-hover);color:rgba(255,255,255,.85);}
.nav-item.active{background:rgba(249,115,22,.15);color:var(--orange);}
.nav-item svg{width:15px;height:15px;flex-shrink:0;opacity:.7;}.nav-item.active svg{opacity:1;}
.nav-dot{width:7px;height:7px;background:var(--orange);border-radius:50%;position:absolute;right:10px;top:50%;transform:translateY(-50%);}
.sidebar-nav{flex:1;overflow-y:auto;padding-bottom:8px;}
.sidebar-footer{padding:12px 16px;border-top:1px solid rgba(255,255,255,.07);}
.supabase-badge{display:flex;align-items:center;gap:8px;}
.pulse-dot{width:7px;height:7px;background:var(--green);border-radius:50%;animation:pulse 2s infinite;flex-shrink:0;}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1);}50%{opacity:.6;transform:scale(1.2);}}

/* ── MAIN ── */
.main{flex:1;display:flex;flex-direction:column;overflow:hidden;min-width:0;}
.topbar{height:56px;background:white;border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 20px;gap:10px;flex-shrink:0;}
.topbar-title{font-size:15px;font-weight:600;color:var(--text);display:flex;align-items:center;gap:8px;flex:1;min-width:0;}
.topbar-breadcrumb{font-size:11.5px;color:var(--sub);display:flex;align-items:center;gap:4px;}
.topbar-breadcrumb span{color:var(--text);font-weight:600;}
.btn{display:flex;align-items:center;gap:6px;padding:7px 14px;border-radius:8px;font-size:12.5px;font-weight:600;cursor:pointer;border:none;font-family:var(--font);transition:all .15s;white-space:nowrap;}
.btn-dark{background:#111827;color:white;}.btn-dark:hover{background:#1F2937;}
.btn-orange{background:var(--orange);color:white;}.btn-orange:hover{background:var(--orange-d);}
.btn-ghost{background:transparent;color:var(--sub);border:1.5px solid var(--border);}.btn-ghost:hover{background:var(--light);}
.btn-teal{background:var(--teal);color:white;}.btn-teal:hover{background:#0D9488;}
.daemon-badge{display:flex;align-items:center;gap:6px;padding:5px 11px;border-radius:20px;background:var(--light);font-size:11px;font-weight:600;color:var(--sub);border:1px solid var(--border);white-space:nowrap;}
.daemon-dot-off{width:7px;height:7px;background:var(--red);border-radius:50%;flex-shrink:0;}
.daemon-dot-on{width:7px;height:7px;background:var(--green);border-radius:50%;animation:pulse 2s infinite;flex-shrink:0;}
.user-badge{display:flex;align-items:center;gap:8px;padding:4px 10px;border-radius:20px;background:var(--light);font-size:12px;font-weight:600;color:var(--text);border:1px solid var(--border);cursor:pointer;white-space:nowrap;}
.user-avatar{width:28px;height:28px;background:#1E3A5F;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;color:white;flex-shrink:0;}
.agents-online{display:flex;align-items:center;gap:6px;padding:5px 12px;border-radius:20px;background:#0F1724;border:1px solid rgba(34,197,94,.4);font-size:11.5px;font-weight:700;color:var(--green);white-space:nowrap;}

/* ── CONTENT ── */
.content{flex:1;overflow-y:auto;padding:20px;}
.view{display:none;}.view.active{display:block;}

.lc-search{padding:8px 14px 8px 14px;border:1.5px solid var(--border);border-radius:10px;font-size:13px;font-family:var(--font);outline:none;background:white;}
.lc-search:focus{border-color:var(--orange);}
.lc-day-bar{display:flex;gap:8px;margin-bottom:16px;overflow-x:auto;padding-bottom:4px;}
.lc-day-btn{display:flex;flex-direction:column;align-items:center;padding:10px 14px;border-radius:12px;border:1.5px solid var(--border);background:white;cursor:pointer;transition:all .15s;min-width:90px;flex-shrink:0;}
.lc-day-btn:hover{border-color:var(--orange);background:#FFF7ED;}
.lc-day-btn.active{border-color:var(--orange);background:var(--orange);color:white;}
.lc-day-label{font-size:11px;font-weight:700;letter-spacing:.3px;}
.lc-day-count{font-size:22px;font-weight:800;line-height:1.1;}
.lc-day-sub{font-size:9.5px;opacity:.75;margin-top:1px;}
.lc-day-btn.active .lc-day-sub{opacity:.8;}
.lc-pagination{display:flex;align-items:center;justify-content:space-between;padding:12px 16px;border-top:1px solid var(--border);background:var(--light);}
.lc-pag-info{font-size:12px;color:var(--sub);}
.lc-pag-btns{display:flex;gap:4px;}
.lc-pag-btn{padding:5px 12px;border-radius:7px;border:1.5px solid var(--border);background:white;cursor:pointer;font-size:12px;font-family:var(--font);font-weight:600;color:var(--sub);transition:all .15s;}
.lc-pag-btn:hover{background:var(--light);}.lc-pag-btn.active{background:var(--text);color:white;border-color:var(--text);}.lc-pag-btn:disabled{opacity:.4;cursor:default;}
/* ── LIFECYCLE ── */
.metric-row{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;margin-bottom:20px;}
.metric-card{background:var(--card);border-radius:16px;padding:20px;display:flex;align-items:center;justify-content:space-between;border:1px solid var(--border);box-shadow:0 1px 4px rgba(0,0,0,.04);}
.metric-val{font-size:36px;font-weight:700;color:var(--text);line-height:1;}
.metric-label{font-size:10px;font-weight:600;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;margin-bottom:4px;}
.metric-icon{width:44px;height:44px;border-radius:12px;display:flex;align-items:center;justify-content:center;}
.mic-orange{background:#FFF7ED;}.mic-green{background:#F0FDF4;}.mic-red{background:#FFF1F2;}
.lifecycle-card{background:var(--card);border-radius:16px;border:1px solid var(--border);overflow:hidden;box-shadow:0 1px 4px rgba(0,0,0,.04);}
.tabs{display:flex;align-items:center;padding:12px 16px;gap:8px;border-bottom:1px solid var(--border);}
.tab{padding:6px 14px;border-radius:20px;font-size:12.5px;font-weight:600;cursor:pointer;transition:all .15s;display:flex;align-items:center;gap:6px;border:1.5px solid transparent;color:var(--sub);}
.tab:hover{background:var(--light);}.tab.active{background:var(--text);color:white;}
.tab-count{font-size:11px;font-weight:700;padding:1px 7px;border-radius:10px;background:rgba(255,255,255,.2);}
.tab:not(.active) .tab-count{background:var(--border);color:var(--sub);}
.tab-spacer{flex:1;}
.table-header{display:grid;padding:9px 16px;border-bottom:1px solid var(--border);background:var(--light);}
.table-header span{font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;}
.table-row{display:grid;padding:13px 16px;border-bottom:1px solid var(--border);align-items:center;transition:background .1s;}
.table-row:hover{background:var(--light);}.table-row:last-child{border-bottom:none;}
.customer-name{font-size:13px;font-weight:600;color:var(--text);}
.customer-id{font-size:10.5px;color:var(--sub);font-family:var(--mono);margin-top:1px;}
.received-time{font-size:12px;color:var(--sub);}
.content-summary{font-size:12.5px;font-weight:500;color:var(--text);}
.content-qty{font-size:11px;color:var(--sub);margin-top:1px;}
.badge{display:inline-flex;align-items:center;gap:5px;padding:4px 10px;border-radius:20px;font-size:11px;font-weight:700;}
.badge svg{width:11px;height:11px;}
.badge-success{background:var(--green-bg);color:var(--green-tx);}
.badge-error{background:var(--red-bg);color:var(--red-tx);}
.badge-pending{background:var(--amber-bg);color:var(--amber-tx);}
.sap-order-chip{display:inline-flex;align-items:center;padding:4px 9px;background:#EFF6FF;border:1.5px solid #BFDBFE;border-radius:8px;font-family:var(--mono);font-size:11px;font-weight:600;color:var(--blue-tx);cursor:pointer;transition:all .15s;}
.sap-order-chip:hover{background:#DBEAFE;}
.action-btns{display:flex;align-items:center;gap:5px;flex-wrap:wrap;}
.action-btn{display:flex;align-items:center;gap:4px;padding:4px 9px;border-radius:7px;font-size:11px;font-weight:600;cursor:pointer;border:1.5px solid;transition:all .15s;font-family:var(--font);white-space:nowrap;}
.ab-sap{border-color:#BFDBFE;color:var(--blue-tx);background:#EFF6FF;}.ab-sap:hover{background:#DBEAFE;}
.ab-vl{border-color:#BBF7D0;color:var(--green-tx);background:#F0FDF4;}.ab-vl:hover{background:var(--green-bg);}
.ab-detail{border-color:var(--border);color:var(--sub);background:white;}.ab-detail:hover{background:var(--light);}
.ab-error{border-color:#FECACA;color:var(--red-tx);background:#FFF1F2;}.ab-error:hover{background:var(--red-bg);}
.ab-fix{border-color:var(--orange);color:var(--orange);background:#FFF7ED;}.ab-fix:hover{background:#FFEDD5;}
.ab-process{border-color:var(--green);color:var(--green-tx);background:var(--green-bg);}.ab-process:hover{background:#BBF7D0;}
.ab-billing{border-color:#EDE9FE;color:var(--purple-tx);background:var(--purple-bg);}.ab-billing:hover{background:#DDD6FE;}
.icon-trash{color:var(--sub);cursor:pointer;padding:4px;border-radius:5px;transition:all .15s;}.icon-trash:hover{background:var(--red-bg);color:var(--red-tx);}
.empty-state{display:flex;flex-direction:column;align-items:center;justify-content:center;padding:60px 20px;color:var(--sub);gap:12px;}
.grid-backlog{grid-template-columns:20px 220px 120px 1fr 120px 260px;}
.grid-success{grid-template-columns:20px 220px 110px 1fr 100px 150px 200px;}
.grid-errors {grid-template-columns:20px 200px 110px 1fr 1fr 120px 180px;}
/* LC status badges */
.lc-badge{display:inline-flex;align-items:center;gap:5px;border-radius:20px;padding:3px 10px;font-size:11px;font-weight:700;letter-spacing:.3px;}
.lc-badge-pending{background:#FEF9C3;color:#92400E;}
.lc-badge-warn   {background:#FEE2E2;color:#991B1B;}
.lc-badge-success{background:#DCFCE7;color:#15803D;}
.lc-badge-error  {background:#FEE2E2;color:#991B1B;}
/* LC filter pills */
.lc-filter-bar{display:flex;align-items:center;gap:10px;margin-bottom:20px;flex-wrap:wrap;}
.lc-pill{display:inline-flex;align-items:center;gap:7px;padding:6px 14px;border-radius:20px;border:1.5px solid var(--border);background:white;font-size:12.5px;font-weight:600;cursor:pointer;color:var(--text);transition:all .15s;}
.lc-pill.active{background:var(--orange);color:white;border-color:var(--orange);}
.lc-pill-count{font-size:11px;font-weight:800;padding:0 6px;border-radius:10px;background:rgba(255,255,255,.25);}
.lc-pill:not(.active) .lc-pill-count{background:var(--border);color:var(--sub);}
.lc-date-input{padding:6px 12px;border:1.5px solid var(--border);border-radius:20px;font-size:12.5px;font-family:var(--font);outline:none;background:white;color:var(--text);}
.lc-date-input:focus{border-color:var(--orange);}
.lc-month-sel{padding:6px 12px;border:1.5px solid var(--border);border-radius:20px;font-size:12.5px;font-family:var(--font);outline:none;background:white;color:var(--text);cursor:pointer;}
.lc-month-sel:focus{border-color:var(--orange);}
/* Action buttons */
.btn-sap{padding:5px 12px;border-radius:8px;border:1.5px solid #16A34A;background:#F0FDF4;color:#16A34A;font-size:11.5px;font-weight:700;cursor:pointer;display:inline-flex;align-items:center;gap:5px;transition:all .15s;}
.btn-sap:hover{background:#16A34A;color:white;}
.btn-warn{padding:5px 12px;border-radius:8px;border:1.5px solid #DC2626;background:#FFF1F0;color:#DC2626;font-size:11.5px;font-weight:700;cursor:pointer;display:inline-flex;align-items:center;gap:5px;transition:all .15s;}
.btn-warn:hover{background:#DC2626;color:white;}
.btn-detail{padding:5px 10px;border-radius:8px;border:1.5px solid var(--border);background:white;color:var(--text);font-size:11.5px;font-weight:600;cursor:pointer;transition:all .15s;}
.btn-detail:hover{border-color:var(--orange);color:var(--orange);}
.btn-kebab{padding:5px 7px;border-radius:8px;border:1.5px solid var(--border);background:white;color:var(--sub);font-size:14px;cursor:pointer;line-height:1;}
.btn-kebab:hover{border-color:var(--orange);color:var(--orange);}
/* Warn correction modal */
.warn-modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.45);z-index:8000;display:none;align-items:center;justify-content:center;}
.warn-modal-overlay.open{display:flex;}
.warn-modal{background:white;border-radius:20px;padding:0;width:520px;max-width:95vw;box-shadow:0 20px 60px rgba(0,0,0,.2);overflow:hidden;}
.warn-modal-head{padding:20px 24px;background:linear-gradient(135deg,#1E293B,#334155);color:white;}
.warn-option{padding:16px 20px;border:1.5px solid var(--border);border-radius:12px;cursor:pointer;transition:all .2s;margin:0 20px 12px;}
.warn-option:hover{border-color:var(--orange);background:#FFF7ED;}
.warn-option.selected{border-color:var(--orange);background:#FFF7ED;}
/* Checkbox style */
.lc-check{width:16px;height:16px;accent-color:var(--orange);cursor:pointer;}

/* ── MODALS ── */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.45);display:none;align-items:center;justify-content:center;z-index:1000;backdrop-filter:blur(4px);}
.modal-overlay.open{display:flex;}
.modal{background:white;border-radius:20px;width:90%;max-width:660px;max-height:88vh;overflow-y:auto;box-shadow:0 24px 60px rgba(0,0,0,.18);animation:modalIn .2s ease;}
@keyframes modalIn{from{transform:scale(.96);opacity:0;}to{transform:scale(1);opacity:1;}}
.modal-header{padding:20px 24px 16px;border-bottom:1px solid var(--border);display:flex;align-items:flex-start;justify-content:space-between;}
.modal-title{font-size:16px;font-weight:700;}.modal-sub{font-size:12px;color:var(--sub);margin-top:2px;}
.modal-close{width:30px;height:30px;border-radius:8px;border:none;background:var(--light);cursor:pointer;font-size:16px;color:var(--sub);display:flex;align-items:center;justify-content:center;}
.modal-close:hover{background:var(--border);}
.modal-body{padding:20px 24px;}.modal-footer{padding:14px 24px;border-top:1px solid var(--border);display:flex;justify-content:flex-end;gap:10px;}
.detail-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
.detail-label{font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;margin-bottom:4px;}
.detail-value{font-size:13px;font-weight:500;color:var(--text);}.detail-value.mono{font-family:var(--mono);font-size:12px;}
.detail-section{margin-bottom:16px;}
.detail-section-title{font-size:12px;font-weight:700;color:var(--text);padding:8px 12px;background:var(--light);border-radius:8px;margin-bottom:10px;display:flex;align-items:center;gap:6px;}
.items-table{width:100%;border-collapse:collapse;font-size:12px;}
.items-table th{text-align:left;padding:7px 10px;background:var(--light);color:var(--sub);font-weight:700;font-size:10px;letter-spacing:.6px;text-transform:uppercase;}
.items-table td{padding:9px 10px;border-bottom:1px solid var(--border);}
.items-table tr:last-child td{border-bottom:none;}
.error-box{background:#FFF1F2;border:1.5px solid #FECACA;border-radius:12px;padding:14px;margin-bottom:14px;}
.error-title{font-size:12.5px;font-weight:700;color:var(--red-tx);display:flex;align-items:center;gap:6px;margin-bottom:8px;}
.error-desc{font-size:12px;color:var(--red-tx);line-height:1.5;}
.ai-sug{background:#F0FDF4;border:1.5px solid #BBF7D0;border-radius:12px;padding:14px;margin-bottom:8px;}
.ai-lbl{font-size:10px;font-weight:700;color:var(--green-tx);letter-spacing:.8px;text-transform:uppercase;margin-bottom:6px;display:flex;align-items:center;gap:5px;}
.ai-sug-text{font-size:12px;color:#166534;line-height:1.5;}
.fix-opt{display:flex;align-items:flex-start;gap:10px;padding:10px 12px;border:1.5px solid var(--border);border-radius:10px;cursor:pointer;transition:all .15s;margin-bottom:7px;}
.fix-opt:hover{border-color:var(--orange);background:#FFF7ED;}

/* ── EMAIL INBOX ── */
.inbox-layout{display:grid;grid-template-columns:330px 1fr;gap:0;height:calc(100vh - 56px - 40px);background:white;border-radius:16px;border:1px solid var(--border);overflow:hidden;}
.email-list-panel{border-right:1px solid var(--border);display:flex;flex-direction:column;}
.email-list-header{padding:14px 16px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;}
.email-search{width:calc(100% - 24px);padding:8px 12px;border:1.5px solid var(--border);border-radius:8px;font-size:12px;font-family:var(--font);outline:none;margin:8px 12px;background:var(--light);}
.email-search:focus{border-color:var(--orange);}
.email-list-body{overflow-y:auto;flex:1;}
.email-item{padding:12px 14px;border-bottom:1px solid var(--border);cursor:pointer;transition:background .1s;position:relative;}
.email-item:hover{background:var(--light);}.email-item.active{background:#FFF7ED;border-left:3px solid var(--orange);}
.email-item.unread .email-item-subject{font-weight:700;}
.email-item-from{font-size:12px;font-weight:600;color:var(--text);display:flex;justify-content:space-between;}
.email-item-time{font-size:10.5px;font-weight:400;color:var(--sub);}
.email-item-subject{font-size:11.5px;color:var(--text);margin:2px 0;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.email-item-preview{font-size:11px;color:var(--sub);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.unread-dot{width:8px;height:8px;background:var(--orange);border-radius:50%;position:absolute;right:14px;top:50%;transform:translateY(-50%);}
.email-detail-panel{display:flex;flex-direction:column;}
.email-detail-header{padding:16px 20px;border-bottom:1px solid var(--border);}
.email-detail-subject{font-size:16px;font-weight:700;margin-bottom:8px;}
.email-detail-body{padding:20px;flex:1;overflow-y:auto;}
.email-body-text{font-size:12.5px;line-height:1.7;color:var(--text);white-space:pre-wrap;font-family:var(--mono);background:var(--light);padding:16px;border-radius:10px;border:1px solid var(--border);}
.ai-parse-panel{margin-top:16px;background:#F0FDF4;border:1.5px solid #BBF7D0;border-radius:12px;padding:16px;}
.ai-parse-title{font-size:12px;font-weight:700;color:var(--green-tx);display:flex;align-items:center;gap:6px;margin-bottom:12px;}
.parse-field-row{display:flex;justify-content:space-between;align-items:center;padding:6px 0;border-bottom:1px solid #BBF7D0;}
.parse-field-row:last-child{border-bottom:none;}
.parse-key{font-size:11px;font-weight:600;color:#166534;}.parse-val{font-size:11.5px;font-weight:500;color:var(--text);font-family:var(--mono);}
.parse-val .ok{color:var(--green-tx);}.parse-val .warn{color:var(--amber-tx);}
.flow-timeline{margin-top:16px;padding:16px;background:var(--light);border-radius:12px;border:1px solid var(--border);}
.flow-title{font-size:11px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;margin-bottom:12px;}
.flow-steps{display:flex;gap:0;align-items:center;}
.flow-step{display:flex;flex-direction:column;align-items:center;gap:4px;flex:1;position:relative;}
.flow-step-circle{width:32px;height:32px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:13px;border:2px solid;transition:all .3s;}
.flow-step.done .flow-step-circle{background:var(--green);border-color:var(--green);color:white;}
.flow-step.active .flow-step-circle{background:var(--orange);border-color:var(--orange);color:white;animation:stepPulse 1.5s infinite;}
.flow-step.pending .flow-step-circle{background:white;border-color:var(--border);color:var(--sub);}
@keyframes stepPulse{0%,100%{box-shadow:0 0 0 0 rgba(249,115,22,.4);}50%{box-shadow:0 0 0 6px rgba(249,115,22,0);}}
.flow-step-label{font-size:9.5px;font-weight:600;color:var(--sub);text-align:center;max-width:60px;line-height:1.3;}
.flow-step.done .flow-step-label,.flow-step.active .flow-step-label{color:var(--text);}
.flow-connector{flex:1;height:2px;background:var(--border);margin-bottom:16px;transition:background .5s;}
.flow-connector.done{background:var(--green);}.flow-connector.active{background:linear-gradient(90deg,var(--green),var(--orange));}
.detail-email-actions{display:flex;gap:10px;padding:14px 20px;border-top:1px solid var(--border);}

/* ── SAP ── */
.sap-view-wrapper{height:calc(100vh - 56px - 40px);display:flex;flex-direction:column;}
.sap-window{background:white;border:1px solid var(--sap-border);border-radius:4px;overflow:hidden;box-shadow:0 2px 12px rgba(0,0,0,.12);display:flex;flex-direction:column;height:100%;}
.sap-titlebar{display:flex;align-items:center;justify-content:space-between;padding:6px 10px;background:linear-gradient(180deg,var(--sap-hdr-top) 0%,var(--sap-hdr-bot) 100%);border-bottom:1px solid var(--sap-border);min-height:36px;}
.sap-titlebar-left{display:flex;align-items:center;gap:8px;}
.sap-titlebar-icon{width:20px;height:20px;border-radius:3px;display:flex;align-items:center;justify-content:center;}
.sap-titlebar-title{font-size:12.5px;font-weight:600;color:var(--sap-navy);font-family:'Arial',sans-serif;}
.sap-win-controls{display:flex;gap:4px;}
.sap-win-btn{width:18px;height:14px;border:1px solid #8BAFC5;border-radius:2px;background:linear-gradient(180deg,#E8EEF4,#C8D8E8);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:10px;color:var(--sap-navy);}
.sap-toolbar{display:flex;align-items:center;gap:2px;padding:4px 10px;background:#E8EEF4;border-bottom:1px solid var(--sap-border);}
.sap-toolbar-btn{width:26px;height:22px;border:1px solid transparent;border-radius:2px;display:flex;align-items:center;justify-content:center;cursor:pointer;font-size:13px;color:#555;transition:all .1s;}
.sap-toolbar-btn:hover{background:#D8E4EE;border-color:#8BAFC5;}
.sap-toolbar-sep{width:1px;height:18px;background:#AABDD0;margin:0 4px;}
.sap-navbar{display:flex;align-items:center;gap:8px;padding:6px 10px;background:#F0F4F8;border-bottom:1px solid var(--sap-border);}
.sap-doc-input{display:flex;align-items:center;gap:0;border:1px solid #8BAFC5;border-radius:2px;overflow:hidden;}
.sap-search-icon{width:24px;height:24px;background:#E0EAF4;border-right:1px solid #8BAFC5;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.sap-doc-field{padding:3px 8px;font-family:'Courier New',monospace;font-size:12px;color:#333;background:white;border:none;outline:none;width:220px;}
.sap-enter-btn{padding:3px 12px;background:linear-gradient(180deg,#E8EEF4,#C8D8E8);border:1px solid #8BAFC5;border-left:none;cursor:pointer;font-size:11.5px;font-family:'Arial',sans-serif;color:var(--sap-navy);}
.sap-btn-pgi{padding:4px 12px;border-radius:2px;font-size:12px;font-family:'Arial',sans-serif;font-weight:600;cursor:pointer;border:1px solid #C05000;background:linear-gradient(180deg,#FF8C3A,#F06800);color:white;display:flex;align-items:center;gap:5px;}
.sap-form-section{padding:10px 12px;border-bottom:1px solid #D8E4EE;background:white;}
.sap-fields-row{display:flex;gap:16px;align-items:flex-start;flex-wrap:wrap;}
.sap-field-group{display:flex;flex-direction:column;gap:2px;}
.sap-field-label{font-size:10.5px;font-family:'Arial',sans-serif;color:#555;font-weight:400;}
.sap-field-input{padding:3px 6px;background:white;border:1px solid #8BAFC5;border-radius:1px;font-family:'Courier New',monospace;font-size:12px;color:#111;outline:none;min-width:80px;}
.sap-field-input.wide{min-width:200px;}.sap-field-input.med{min-width:130px;}.sap-field-input.narrow{min-width:60px;max-width:75px;}
.sap-field-inline{display:flex;gap:0;}
.sap-field-inline .sap-field-input{border-right:none;}.sap-field-inline .sap-field-input:last-child{border-right:1px solid #8BAFC5;}
.sap-field-name{padding:3px 8px;background:#E8EEF4;border:1px solid #8BAFC5;border-left:none;font-family:'Arial',sans-serif;font-size:12px;color:#333;min-width:180px;}
.sap-tabs{display:flex;align-items:flex-end;padding:0 10px;background:#EEF2F7;border-bottom:2px solid var(--sap-border);gap:0;flex-shrink:0;}
.sap-tab{padding:6px 14px;font-family:'Arial',sans-serif;font-size:12px;color:#555;cursor:pointer;border:1px solid transparent;border-bottom:none;margin-bottom:-2px;background:transparent;position:relative;transition:all .1s;white-space:nowrap;}
.sap-tab:hover{background:#E0E8F0;color:var(--sap-navy);}
.sap-tab.active{background:white;color:var(--sap-navy);font-weight:700;border:1px solid var(--sap-border);border-bottom:2px solid white;border-radius:3px 3px 0 0;}
.sap-subsection{padding:10px 12px;border-bottom:1px solid #D8E4EE;background:white;}
.sap-subsection-title{font-size:10.5px;font-family:'Arial',sans-serif;font-weight:700;color:var(--sap-navy);margin-bottom:6px;text-transform:uppercase;letter-spacing:.4px;}
.sap-table-wrapper{flex:1;overflow:auto;background:white;}
.sap-table{width:100%;border-collapse:collapse;font-family:'Arial',sans-serif;font-size:12px;}
.sap-table th{padding:5px 10px;background:linear-gradient(180deg,#E8EEF4,#D4E2EE);border:1px solid var(--sap-border);color:var(--sap-navy);font-weight:700;text-align:left;white-space:nowrap;font-size:11.5px;position:sticky;top:0;z-index:2;}
.sap-table td{padding:4px 10px;border:1px solid #D8E8F4;color:#111;white-space:nowrap;}
.sap-table tr:nth-child(even) td{background:#EEF4F9;}
.sap-table tr:hover td{background:#D8EEF8;}
.sap-link{color:#0064A3;text-decoration:underline;cursor:pointer;}
.sap-tab-content{display:none;flex:1;overflow:hidden;}.sap-tab-content.active{display:flex;flex-direction:column;}
.sap-statusbar{display:flex;align-items:center;gap:8px;padding:4px 10px;background:#F0F4F8;border-top:1px solid var(--sap-border);min-height:28px;flex-shrink:0;}
.sap-status-icon{width:18px;height:18px;border-radius:3px;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;flex-shrink:0;}
.sap-status-ok{background:#4CAF50;color:white;}.sap-status-warn{background:#FF9800;color:white;}
.sap-status-text{font-family:'Arial',sans-serif;font-size:12px;color:#333;}

/* ── AI CONTROL TOWER ── */
.ct-layout{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
.ct-card{background:var(--navy-dark);border-radius:16px;padding:20px;color:white;}
.ct-card-wide{grid-column:1/-1;}
.ct-header{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:16px;}
.ct-title{font-size:14px;font-weight:700;display:flex;align-items:center;gap:8px;}
.ct-subtitle{font-size:10px;color:rgba(255,255,255,.4);margin-top:2px;letter-spacing:.8px;text-transform:uppercase;}
.ct-metric{background:rgba(255,255,255,.06);border-radius:12px;padding:14px;}
.ct-metric-label{font-size:9.5px;color:rgba(255,255,255,.4);letter-spacing:.8px;text-transform:uppercase;margin-bottom:6px;display:flex;align-items:center;gap:5px;}
.ct-metric-val{font-size:24px;font-weight:700;}
.ct-ai-box{background:rgba(249,115,22,.12);border:1.5px solid rgba(249,115,22,.3);border-radius:12px;padding:16px;margin-bottom:14px;}
.ct-ai-label{font-size:10px;font-weight:700;color:var(--orange);letter-spacing:.8px;text-transform:uppercase;margin-bottom:8px;}
.ct-ai-text{font-size:12px;color:rgba(255,255,255,.75);line-height:1.6;}
.ct-btn{display:flex;align-items:center;gap:6px;padding:7px 12px;border-radius:8px;font-size:11.5px;font-weight:600;cursor:pointer;border:1.5px solid rgba(255,255,255,.15);color:rgba(255,255,255,.7);background:rgba(255,255,255,.06);font-family:var(--font);transition:all .15s;}
.ct-btn:hover{background:rgba(255,255,255,.12);color:white;}
.filter-select{padding:7px 12px;border:1.5px solid var(--border);border-radius:8px;font-size:12px;font-family:var(--font);background:white;color:var(--text);outline:none;cursor:pointer;}
.filter-select:focus{border-color:var(--orange);}
.sla-row{margin-bottom:12px;}
.sla-row-top{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:5px;gap:8px;}
.sla-row-label{font-size:11px;font-weight:500;color:rgba(255,255,255,.75);line-height:1.35;max-width:65%;}
.sla-row-right{display:flex;flex-direction:column;align-items:flex-end;gap:2px;}
.sla-row-pct{font-size:13px;font-weight:800;white-space:nowrap;}
.sla-row-target{font-size:9px;color:rgba(255,255,255,.35);white-space:nowrap;}
.sla-track{height:6px;background:rgba(255,255,255,.1);border-radius:4px;overflow:hidden;}
.sla-fill{height:100%;border-radius:4px;transition:width 1s ease;}
.bar-chart{display:flex;align-items:flex-end;gap:6px;height:80px;margin-top:8px;}
.bar{flex:1;border-radius:4px 4px 0 0;transition:all .5s;position:relative;cursor:pointer;}
.bar:hover{opacity:.85;}
.bar-val{position:absolute;top:-18px;left:50%;transform:translateX(-50%);font-size:9px;font-weight:700;color:rgba(255,255,255,.7);white-space:nowrap;}

/* ══════════════════════════════════════ */
/*  MODULE 5 — AGENT OBSERVATORY         */
/* ══════════════════════════════════════ */
.obs-layout{display:grid;grid-template-columns:280px 1fr;gap:0;height:calc(100vh - 56px - 40px);background:var(--obs-bg);border-radius:16px;overflow:hidden;border:1px solid var(--obs-border);}
.obs-sidebar{border-right:1px solid var(--obs-border);display:flex;flex-direction:column;}
.obs-sidebar-header{padding:16px;border-bottom:1px solid var(--obs-border);}
.obs-search{width:100%;padding:8px 12px;background:rgba(255,255,255,.06);border:1px solid var(--obs-border);border-radius:8px;font-size:12px;font-family:var(--font);color:var(--obs-text);outline:none;}
.obs-search::placeholder{color:var(--obs-sub);}
.obs-search:focus{border-color:var(--teal);}
.obs-agent-list{overflow-y:auto;flex:1;}
.obs-agent-item{display:flex;align-items:center;gap:10px;padding:10px 16px;cursor:pointer;transition:background .1s;border-left:3px solid transparent;}
.obs-agent-item:hover{background:rgba(255,255,255,.05);}
.obs-agent-item.active{background:rgba(20,184,166,.08);border-left-color:var(--teal);}
.obs-agent-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;}
.obs-agent-dot.running{background:var(--green);animation:pulse 2s infinite;}
.obs-agent-dot.idle{background:var(--sub);}
.obs-agent-dot.error{background:var(--red);animation:pulse 1s infinite;}
.obs-agent-name{font-size:12.5px;color:var(--obs-text);font-weight:400;}
.obs-agent-item.active .obs-agent-name{font-weight:600;color:white;}
.obs-agent-chevron{margin-left:auto;color:var(--obs-sub);font-size:12px;}
.obs-main{display:flex;flex-direction:column;overflow-y:auto;}
.obs-main-header{padding:24px 28px 20px;border-bottom:1px solid var(--obs-border);}
.obs-agent-title{font-size:22px;font-weight:700;color:white;margin-bottom:8px;}
.obs-status-row{display:flex;align-items:center;gap:16px;}
.obs-running-badge{display:inline-flex;align-items:center;gap:6px;padding:4px 12px;border-radius:20px;font-size:11px;font-weight:700;letter-spacing:.6px;}
.obs-badge-running{background:rgba(34,197,94,.15);color:var(--green);border:1px solid rgba(34,197,94,.3);}
.obs-badge-idle{background:rgba(107,114,128,.15);color:var(--obs-sub);border:1px solid rgba(107,114,128,.3);}
.obs-badge-error{background:rgba(239,68,68,.15);color:var(--red);border:1px solid rgba(239,68,68,.3);}
.obs-stat{display:flex;flex-direction:column;align-items:center;}
.obs-stat-val{font-size:20px;font-weight:800;color:var(--teal);}
.obs-stat-lbl{font-size:9.5px;color:var(--obs-sub);letter-spacing:.8px;text-transform:uppercase;margin-top:2px;}
.obs-main-body{padding:24px 28px;display:grid;grid-template-columns:1fr 340px;gap:16px;}
.obs-card{background:var(--obs-card);border:1px solid var(--obs-border);border-radius:12px;padding:18px;margin-bottom:14px;}
.obs-card:last-child{margin-bottom:0;}
.obs-card-title{display:flex;align-items:center;gap:10px;margin-bottom:14px;}
.obs-card-icon{width:32px;height:32px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:15px;flex-shrink:0;}
.obs-card-title-text{font-size:14px;font-weight:700;color:white;}
.obs-card-sub{font-size:12px;color:var(--obs-sub);line-height:1.5;}
.obs-bullet{display:flex;align-items:flex-start;gap:8px;padding:6px 0;border-bottom:1px solid var(--obs-border);font-size:12px;color:var(--obs-sub);}
.obs-bullet:last-child{border-bottom:none;}
.obs-bullet-dot{width:6px;height:6px;border-radius:50%;background:var(--teal);flex-shrink:0;margin-top:5px;}
.obs-constraint-row{display:flex;align-items:center;gap:10px;padding:7px 10px;background:rgba(255,255,255,.04);border-radius:8px;margin-bottom:6px;}
.obs-ai-chip{width:24px;height:24px;border-radius:6px;background:rgba(20,184,166,.2);border:1px solid rgba(20,184,166,.3);display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:700;color:var(--teal);flex-shrink:0;}
.obs-constraint-text{font-size:12px;color:var(--obs-text);}
.obs-inference-empty{padding:24px;text-align:center;color:var(--obs-sub);font-size:12px;font-style:italic;}
.obs-log-row{padding:6px 0;border-bottom:1px solid var(--obs-border);display:flex;gap:10px;font-size:11.5px;}
.obs-log-time{font-family:var(--mono);color:var(--obs-sub);white-space:nowrap;font-size:10.5px;}
.obs-log-text{color:var(--obs-text);}
.obs-log-ok{color:var(--green);}
.obs-log-warn{color:var(--amber);}
.obs-log-err{color:var(--red);}

/* ══════════════════════════════════════ */
/*  MODULE 6 — BUSINESS RULES ADMIN      */
/* ══════════════════════════════════════ */
.admin-layout{display:grid;grid-template-columns:1fr 1fr;gap:16px;}
.admin-card{background:white;border:1px solid var(--border);border-radius:16px;padding:0;overflow:hidden;box-shadow:0 1px 4px rgba(0,0,0,.04);}
.admin-card-header{padding:18px 20px 14px;border-bottom:1px solid var(--border);}
.admin-card-title{font-size:16px;font-weight:700;color:var(--text);display:flex;align-items:center;gap:10px;margin-bottom:3px;}
.admin-card-title svg{width:18px;height:18px;color:var(--orange);}
.admin-card-sub{font-size:12px;color:var(--sub);}
.admin-agent-row{display:flex;align-items:center;padding:14px 20px;border-bottom:1px solid var(--border);transition:background .1s;}
.admin-agent-row:hover{background:var(--light);}
.admin-agent-row:last-child{border-bottom:none;}
.admin-agent-name{font-size:13px;font-weight:600;color:var(--text);flex:1;}
.admin-agent-status{font-size:9.5px;font-weight:700;padding:2px 7px;border-radius:4px;letter-spacing:.5px;text-transform:uppercase;margin-left:8px;}
.admin-status-running{background:var(--green-bg);color:var(--green-tx);}
.admin-status-idle{background:var(--light);color:var(--sub);}
.admin-agent-version{font-size:10px;color:var(--sub);margin-left:6px;}
.admin-logs-btn{display:flex;align-items:center;gap:6px;padding:5px 12px;border-radius:7px;font-size:11.5px;font-weight:600;cursor:pointer;border:1.5px solid var(--border);color:var(--sub);background:white;font-family:var(--font);transition:all .15s;white-space:nowrap;}
.admin-logs-btn:hover{background:var(--light);border-color:var(--sub);}
.admin-rule-row{display:flex;align-items:flex-start;justify-content:space-between;padding:16px 20px;border-bottom:1px solid var(--border);transition:background .1s;}
.admin-rule-row:hover{background:var(--light);}
.admin-rule-row:last-of-type{border-bottom:none;}
.admin-rule-title{font-size:13px;font-weight:600;color:var(--text);margin-bottom:4px;}
.admin-rule-desc{font-size:12px;color:var(--sub);line-height:1.45;max-width:90%;}
.admin-rule-edit{width:32px;height:32px;border-radius:8px;border:1px solid var(--border);background:white;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .15s;flex-shrink:0;}
.admin-rule-edit:hover{background:var(--light);border-color:var(--sub);}
.admin-add-rule{display:flex;align-items:center;gap:8px;padding:14px 20px;cursor:pointer;color:var(--sub);font-size:13px;font-weight:500;transition:all .15s;border-top:1px solid var(--border);}
.admin-add-rule:hover{background:var(--light);color:var(--text);}
.admin-editable-input{width:100%;padding:6px 10px;border:1.5px solid var(--border);border-radius:8px;font-size:12.5px;font-family:var(--font);outline:none;color:var(--text);background:white;}
.admin-editable-input:focus{border-color:var(--orange);}
.admin-switch{position:relative;width:40px;height:22px;flex-shrink:0;}
.admin-switch input{opacity:0;width:0;height:0;}
.admin-switch-slider{position:absolute;cursor:pointer;inset:0;background:#D1D5DB;border-radius:22px;transition:.3s;}
.admin-switch-slider:before{position:absolute;content:'';height:16px;width:16px;left:3px;bottom:3px;background:white;border-radius:50%;transition:.3s;}
.admin-switch input:checked + .admin-switch-slider{background:var(--orange);}
.admin-switch input:checked + .admin-switch-slider:before{transform:translateX(18px);}

/* ── ATTACHMENTS PANEL ── */
.attach-panel{margin-top:16px;border:1.5px solid var(--border);border-radius:12px;overflow:hidden;}
.attach-header{display:flex;align-items:center;justify-content:space-between;padding:12px 16px;background:var(--light);border-bottom:1px solid var(--border);}
.attach-title{font-size:12px;font-weight:700;color:var(--text);display:flex;align-items:center;gap:7px;}
.attach-count{font-size:10px;padding:2px 7px;border-radius:10px;background:var(--border);color:var(--sub);font-weight:700;}
.attach-list{padding:10px 14px;display:flex;flex-direction:column;gap:8px;}
.attach-item{display:flex;align-items:center;gap:12px;padding:10px 14px;border:1.5px solid var(--border);border-radius:10px;background:white;transition:all .15s;cursor:pointer;}
.attach-item:hover{border-color:var(--orange);background:#FFF7ED;}
.attach-icon{width:38px;height:38px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;}
.attach-icon-xlsx{background:#E8F5E9;}
.attach-icon-pdf{background:#FDE8E8;}
.attach-icon-msg{background:#E8EEF9;}
.attach-meta{flex:1;min-width:0;}
.attach-name{font-size:12.5px;font-weight:600;color:var(--text);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.attach-size{font-size:11px;color:var(--sub);margin-top:2px;}
.attach-actions{display:flex;gap:6px;flex-shrink:0;}
.attach-btn{display:flex;align-items:center;gap:5px;padding:5px 10px;border-radius:7px;font-size:11px;font-weight:600;cursor:pointer;border:1.5px solid;transition:all .15s;font-family:var(--font);}
.attach-btn-view{border-color:var(--blue);color:var(--blue-tx);background:var(--blue-bg);}.attach-btn-view:hover{background:#BFDBFE;}
.attach-btn-dl{border-color:var(--border);color:var(--sub);background:white;}.attach-btn-dl:hover{background:var(--light);}

/* ── PO VIEWER MODAL ── */
.po-modal{max-width:860px!important;}
.po-header-band{background:linear-gradient(135deg,#003366 0%,#0064A3 100%);padding:20px 24px;color:white;}
.po-header-band-top{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:12px;}
.po-brand{font-size:22px;font-weight:800;letter-spacing:1px;}
.po-brand-sub{font-size:10px;letter-spacing:2px;opacity:.7;text-transform:uppercase;margin-top:2px;}
.po-badge{display:inline-flex;align-items:center;gap:6px;padding:6px 14px;border-radius:20px;background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.3);font-size:12px;font-weight:700;}
.po-meta-row{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-top:14px;border-top:1px solid rgba(255,255,255,.2);padding-top:14px;}
.po-meta-item{display:flex;flex-direction:column;gap:2px;}
.po-meta-lbl{font-size:9px;font-weight:700;letter-spacing:1px;text-transform:uppercase;opacity:.6;}
.po-meta-val{font-size:13px;font-weight:700;}
.po-body{padding:0;}
.po-section-title{font-size:11px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;padding:14px 20px 8px;background:var(--light);border-bottom:1px solid var(--border);}
.po-table{width:100%;border-collapse:collapse;font-size:12.5px;}
.po-table th{text-align:left;padding:9px 14px;background:#EFF6FF;color:var(--blue-tx);font-weight:700;font-size:10.5px;letter-spacing:.6px;text-transform:uppercase;border-bottom:2px solid #BFDBFE;}
.po-table td{padding:10px 14px;border-bottom:1px solid var(--border);vertical-align:middle;}
.po-table tr:last-child td{border-bottom:none;}
.po-table tr:hover td{background:#FAFBFF;}
.po-table .sku-chip{display:inline-block;padding:2px 8px;background:#EFF6FF;border:1px solid #BFDBFE;border-radius:5px;font-family:var(--mono);font-size:11px;color:var(--blue-tx);}
.po-total-row{background:#F0F9FF;font-weight:700;}
.po-total-row td{border-top:2px solid #BFDBFE!important;padding:12px 14px;}
.po-footer-section{padding:14px 20px;background:var(--light);border-top:1px solid var(--border);}
.po-conditions{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.po-condition{display:flex;align-items:flex-start;gap:8px;font-size:11.5px;color:var(--sub);}
.po-condition-icon{font-size:15px;flex-shrink:0;}

/* ── REPOSITORIO ── */
.repo-toolbar{display:flex;align-items:center;gap:12px;margin-bottom:20px;flex-wrap:wrap;}
.repo-search{flex:1;min-width:200px;padding:9px 14px 9px 36px;border:1.5px solid var(--border);border-radius:10px;font-size:13px;font-family:var(--font);outline:none;background:white;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' fill='none' stroke='%236B7280' stroke-width='2'%3E%3Ccircle cx='7' cy='7' r='5'/%3E%3Cline x1='14' y1='14' x2='10.5' y2='10.5'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:10px center;}
.repo-search:focus{border-color:var(--orange);}
.repo-filter{padding:9px 14px;border:1.5px solid var(--border);border-radius:10px;font-size:13px;font-family:var(--font);background:white;outline:none;cursor:pointer;}
.repo-filter:focus{border-color:var(--orange);}
.repo-stats{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:20px;}
.repo-stat-card{background:white;border:1px solid var(--border);border-radius:14px;padding:16px 20px;display:flex;align-items:center;justify-content:space-between;box-shadow:0 1px 4px rgba(0,0,0,.04);}
.repo-stat-val{font-size:28px;font-weight:800;color:var(--text);line-height:1;}
.repo-stat-lbl{font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;margin-bottom:3px;}
.repo-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:16px;}
.repo-doc-card{background:white;border:1px solid var(--border);border-radius:14px;overflow:hidden;box-shadow:0 1px 4px rgba(0,0,0,.04);transition:all .2s;cursor:pointer;}
.repo-doc-card:hover{box-shadow:0 4px 16px rgba(0,0,0,.1);transform:translateY(-2px);border-color:var(--orange);}
.repo-doc-preview{height:100px;display:flex;align-items:center;justify-content:center;font-size:48px;position:relative;overflow:hidden;}
.repo-doc-preview-xlsx{background:linear-gradient(135deg,#E8F5E9,#C8E6C9);}
.repo-doc-preview-pdf{background:linear-gradient(135deg,#FFEBEE,#FFCDD2);}
.repo-doc-preview-msg{background:linear-gradient(135deg,#E8EAF6,#C5CAE9);}
.repo-doc-preview-lines{position:absolute;bottom:10px;left:50%;transform:translateX(-50%);display:flex;flex-direction:column;gap:3px;width:70%;}
.repo-doc-preview-line{height:4px;border-radius:2px;background:rgba(0,0,0,.12);}
.repo-doc-card-body{padding:14px;}
.repo-doc-name{font-size:12.5px;font-weight:700;color:var(--text);margin-bottom:4px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.repo-doc-meta{font-size:11px;color:var(--sub);display:flex;justify-content:space-between;margin-bottom:8px;}
.repo-doc-tags{display:flex;gap:5px;flex-wrap:wrap;margin-bottom:10px;}
.repo-doc-tag{padding:2px 8px;border-radius:6px;font-size:10px;font-weight:700;}
.repo-doc-tag-po{background:#EFF6FF;color:var(--blue-tx);}
.repo-doc-tag-pdf{background:#FFF1F2;color:var(--red-tx);}
.repo-doc-tag-xlsx{background:#F0FDF4;color:var(--green-tx);}
.repo-doc-tag-msg{background:#EEF2FF;color:var(--purple-tx);}
.repo-doc-tag-proc{background:var(--green-bg);color:var(--green-tx);}
.repo-doc-tag-pend{background:var(--amber-bg);color:var(--amber-tx);}
.repo-doc-actions{display:flex;gap:6px;}
.repo-btn{display:flex;align-items:center;gap:5px;padding:6px 12px;border-radius:8px;font-size:11.5px;font-weight:600;cursor:pointer;border:1.5px solid;transition:all .15s;font-family:var(--font);flex:1;justify-content:center;}
.repo-btn-open{border-color:var(--orange);color:var(--orange);background:#FFF7ED;}.repo-btn-open:hover{background:#FFEDD5;}
.repo-btn-dl{border-color:var(--border);color:var(--sub);background:white;}.repo-btn-dl:hover{background:var(--light);}

/* ── PDF VIEWER MODAL ── */
.pdf-modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.75);display:none;flex-direction:column;z-index:2000;backdrop-filter:blur(4px);}
.pdf-modal-overlay.open{display:flex;}
.pdf-viewer-toolbar{background:#1F2937;padding:12px 20px;display:flex;align-items:center;gap:12px;flex-shrink:0;}
.pdf-viewer-title{color:white;font-size:13px;font-weight:600;flex:1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.pdf-tb-btn{display:flex;align-items:center;gap:6px;padding:7px 14px;border-radius:8px;font-size:12px;font-weight:600;cursor:pointer;border:1.5px solid rgba(255,255,255,.2);color:rgba(255,255,255,.8);background:rgba(255,255,255,.08);font-family:var(--font);transition:all .15s;}
.pdf-tb-btn:hover{background:rgba(255,255,255,.15);color:white;}
.pdf-tb-btn-orange{border-color:var(--orange);color:var(--orange);background:rgba(249,115,22,.1);}.pdf-tb-btn-orange:hover{background:rgba(249,115,22,.2);}
.pdf-viewer-body{flex:1;overflow-y:auto;background:#525659;display:flex;justify-content:center;padding:32px 20px;gap:24px;} .pdf-viewer-body.oracle-mode{background:#E8E8E8;padding:20px;display:block;}
.pdf-page{background:white;width:794px;min-height:1123px;box-shadow:0 8px 32px rgba(0,0,0,.4);border-radius:2px;flex-shrink:0;display:flex;flex-direction:column;padding:60px 70px;position:relative;}
.pdf-page-number{position:absolute;bottom:24px;right:32px;font-size:10px;color:#999;font-family:'Times New Roman',serif;}
/* PDF Document styles */
.pdf-doc-header{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:32px;padding-bottom:20px;border-bottom:3px solid #003366;}
.pdf-doc-logo-text{font-size:32px;font-weight:900;color:#003366;letter-spacing:2px;line-height:1;}
.pdf-doc-logo-sub{font-size:9px;color:#666;letter-spacing:2px;text-transform:uppercase;margin-top:3px;}
.pdf-doc-title-block{text-align:right;}
.pdf-doc-title{font-size:18px;font-weight:800;color:#003366;text-transform:uppercase;letter-spacing:1px;}
.pdf-doc-subtitle{font-size:10px;color:#666;margin-top:3px;letter-spacing:1px;}
.pdf-doc-po-number{font-size:14px;font-weight:700;color:#003366;margin-top:6px;font-family:'Courier New',monospace;}
.pdf-info-grid{display:grid;grid-template-columns:1fr 1fr;gap:0;margin-bottom:24px;border:1px solid #E0E0E0;}
.pdf-info-cell{padding:10px 14px;border-bottom:1px solid #E0E0E0;border-right:1px solid #E0E0E0;}
.pdf-info-cell:nth-child(even){border-right:none;}
.pdf-info-cell:nth-last-child(-n+2){border-bottom:none;}
.pdf-info-label{font-size:8.5px;font-weight:700;color:#003366;letter-spacing:1px;text-transform:uppercase;margin-bottom:3px;}
.pdf-info-value{font-size:12px;font-weight:600;color:#1A1A1A;}
.pdf-table-section{margin-bottom:24px;}
.pdf-section-header{background:#003366;color:white;padding:8px 14px;font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;margin-bottom:0;}
.pdf-doc-table{width:100%;border-collapse:collapse;font-size:11px;}
.pdf-doc-table th{background:#EEF4FF;padding:8px 10px;text-align:left;font-size:9px;font-weight:700;color:#003366;letter-spacing:.8px;text-transform:uppercase;border:1px solid #D0DCF0;}
.pdf-doc-table td{padding:9px 10px;border:1px solid #E8EEF8;vertical-align:middle;color:#1A1A1A;}
.pdf-doc-table tr:nth-child(even) td{background:#F8FAFF;}
.pdf-total-section{background:#EEF4FF;border:1px solid #D0DCF0;padding:14px;margin-bottom:20px;display:flex;justify-content:flex-end;}
.pdf-total-table{min-width:260px;}
.pdf-total-row{display:flex;justify-content:space-between;padding:4px 0;font-size:12px;border-bottom:1px solid #D0DCF0;}
.pdf-total-row:last-child{border-bottom:none;font-size:14px;font-weight:800;color:#003366;padding-top:8px;}
.pdf-conditions-section{margin-bottom:24px;}
.pdf-conditions-box{border:1px solid #E0E0E0;border-radius:4px;padding:14px;}
.pdf-condition-item{display:flex;align-items:flex-start;gap:8px;font-size:10.5px;color:#444;padding:5px 0;border-bottom:1px solid #F0F0F0;}
.pdf-condition-item:last-child{border-bottom:none;}
.pdf-condition-bullet{width:18px;height:18px;background:#003366;border-radius:3px;display:flex;align-items:center;justify-content:center;font-size:9px;font-weight:700;color:white;flex-shrink:0;margin-top:1px;}
.pdf-signatures{display:grid;grid-template-columns:1fr 1fr;gap:40px;margin-top:32px;border-top:1px solid #E0E0E0;padding-top:24px;}
.pdf-sig-block{display:flex;flex-direction:column;align-items:center;}
.pdf-sig-line{width:100%;height:1px;background:#333;margin-bottom:6px;margin-top:40px;}
.pdf-sig-name{font-size:10.5px;font-weight:700;color:#1A1A1A;text-align:center;}
.pdf-sig-role{font-size:9px;color:#666;text-align:center;margin-top:2px;}
.pdf-footer{border-top:2px solid #003366;padding-top:12px;margin-top:auto;display:flex;justify-content:space-between;align-items:center;}
.pdf-footer-left{font-size:8.5px;color:#999;line-height:1.6;}
.pdf-footer-right{font-size:8.5px;color:#003366;font-weight:700;}

/* ── LIFECYCLE DAY FILTER & PAGINATION ── */
.lc-day-bar{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:16px;}
.lc-day-btn{display:flex;flex-direction:column;align-items:center;padding:8px 10px;background:white;border:1.5px solid var(--border);border-radius:10px;cursor:pointer;transition:all .15s;min-width:52px;}
.lc-day-btn:hover{background:var(--light);border-color:var(--sub);}
.lc-day-btn.active{border-width:2px;}
.lc-day-short{font-size:10px;font-weight:700;color:var(--sub);text-transform:uppercase;letter-spacing:.5px;}
.lc-day-n{font-size:16px;font-weight:700;color:var(--text);line-height:1.2;}
.lc-filter-row{display:flex;align-items:center;gap:8px;padding:10px 16px;border-bottom:1px solid var(--border);background:var(--light);}
.lc-search{flex:1;padding:7px 12px;border:1.5px solid var(--border);border-radius:8px;font-size:12px;font-family:var(--font);outline:none;background:white;}
.lc-search:focus{border-color:var(--orange);}
.lc-pag-row{display:flex;align-items:center;justify-content:center;gap:16px;padding:14px;border-top:1px solid var(--border);}
.lc-pag-btn{padding:7px 16px;border-radius:8px;border:1.5px solid var(--border);background:white;font-size:12.5px;font-weight:600;cursor:pointer;font-family:var(--font);transition:all .15s;}
.lc-pag-btn:hover:not([disabled]){background:var(--light);}
.lc-pag-btn[disabled]{opacity:.4;cursor:default;}
.lc-pag-info{font-size:12px;color:var(--sub);font-weight:500;}
#lc-pagination{background:var(--card);}

/* ── REPORTES ── */
.rpt-header{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:20px;flex-wrap:wrap;gap:12px;}
.rpt-kpi-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:20px;}
.rpt-kpi{background:white;border:1px solid var(--border);border-radius:16px;padding:18px 20px;box-shadow:0 1px 4px rgba(0,0,0,.04);position:relative;overflow:hidden;}
.rpt-kpi::after{content:'';position:absolute;bottom:0;left:0;right:0;height:3px;}
.rpt-kpi.green::after{background:var(--green);} .rpt-kpi.red::after{background:var(--red);}
.rpt-kpi.orange::after{background:var(--orange);} .rpt-kpi.blue::after{background:var(--blue);}
.rpt-kpi-val{font-size:32px;font-weight:800;color:var(--text);line-height:1;}
.rpt-kpi-label{font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;margin-bottom:4px;}
.rpt-kpi-sub{font-size:11px;color:var(--sub);margin-top:4px;}
.rpt-grid2{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:16px;}
.rpt-card{background:white;border:1px solid var(--border);border-radius:16px;padding:20px;box-shadow:0 1px 4px rgba(0,0,0,.04);}
.rpt-card-title{font-size:13px;font-weight:700;color:var(--text);margin-bottom:14px;display:flex;align-items:center;gap:8px;}
.rpt-bar-row{display:flex;align-items:center;gap:10px;margin-bottom:8px;}
.rpt-bar-label{font-size:12px;color:var(--text);min-width:160px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.rpt-bar-track{flex:1;height:10px;background:var(--light);border-radius:5px;overflow:hidden;}
.rpt-bar-fill{height:100%;border-radius:5px;transition:width .8s;}
.rpt-bar-val{font-size:11.5px;font-weight:700;color:var(--text);min-width:50px;text-align:right;}
.rpt-10day-chart{display:flex;align-items:flex-end;gap:8px;height:140px;margin-top:12px;padding:0 4px;}
.rpt-day-col{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px;}
.rpt-day-bar{width:100%;border-radius:4px 4px 0 0;position:relative;transition:all .5s;cursor:pointer;}
.rpt-day-bar:hover{opacity:.8;}
.rpt-day-bar-val{position:absolute;top:-16px;left:50%;transform:translateX(-50%);font-size:9.5px;font-weight:700;color:var(--text);white-space:nowrap;}
.rpt-day-label{font-size:9px;font-weight:600;color:var(--sub);text-align:center;margin-top:2px;}
.rpt-err-type{display:flex;justify-content:space-between;align-items:center;padding:8px 0;border-bottom:1px solid var(--border);}
.rpt-err-type:last-child{border-bottom:none;}
.rpt-err-badge{font-size:10.5px;font-weight:700;padding:3px 8px;border-radius:6px;background:var(--red-bg);color:var(--red-tx);}
.rpt-trend-row{display:flex;align-items:center;gap:8px;padding:7px 0;border-bottom:1px solid var(--border);font-size:12px;}
.rpt-trend-row:last-child{border-bottom:none;}
.rpt-trend-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0;}

/* ── TOAST ── */
.toast{position:fixed;bottom:24px;right:24px;z-index:2000;background:#111827;color:white;padding:12px 18px;border-radius:10px;font-size:13px;font-weight:500;box-shadow:0 8px 24px rgba(0,0,0,.25);display:flex;align-items:center;gap:8px;animation:toastIn .3s ease;max-width:340px;}
.toast.hidden{display:none;}
@keyframes toastIn{from{transform:translateY(20px);opacity:0;}to{transform:translateY(0);opacity:1;}}
.ct-metric{background:rgba(255,255,255,.06);border-radius:10px;padding:12px;}
.ct-metric-lbl{font-size:9px;color:rgba(255,255,255,.4);text-transform:uppercase;letter-spacing:.8px;margin-bottom:3px;}
.ct-metric-val{font-size:20px;font-weight:800;color:white;}
/* Date filter */
input[type="date"]::-webkit-calendar-picker-indicator{opacity:.5;cursor:pointer;}

/* ═══════════════════════════════════════════
   SAP GUI — Authentic Look & Feel (v2)
   ══════════════════════════════════════════ */
:root{
  --sap-hdr-top:#F5F7FA; --sap-hdr-bot:#E0EAF4;
  --sap-border:#A0B8CC;  --sap-navy:#003366;
  --sap-blue:#0064A3;    --sap-amber:#C05000;
  --sap-green:#006400;
}
.sap-wrap{height:calc(100vh - 56px - 40px);display:flex;flex-direction:column;}
.sap-window{
  background:white;border:1px solid var(--sap-border);
  border-radius:3px;overflow:hidden;
  box-shadow:0 3px 14px rgba(0,0,0,.14);
  display:flex;flex-direction:column;height:100%;
}
/* Title bar */
.sap-titlebar{
  display:flex;align-items:center;justify-content:space-between;
  padding:5px 10px;
  background:linear-gradient(180deg,var(--sap-hdr-top) 0%,var(--sap-hdr-bot) 100%);
  border-bottom:1px solid var(--sap-border);flex-shrink:0;min-height:34px;
}
.sap-titlebar-left{display:flex;align-items:center;gap:8px;}
.sap-win-icon{
  width:22px;height:22px;border-radius:3px;
  display:flex;align-items:center;justify-content:center;font-size:13px;
}
.sap-win-title{font-size:13px;font-weight:700;color:var(--sap-navy);font-family:Arial,sans-serif;}
.sap-wbtns{display:flex;gap:3px;}
.sap-wb{
  width:16px;height:14px;border:1px solid #8BAFC5;border-radius:2px;
  background:linear-gradient(180deg,#E8EEF4,#C8D8E8);
  cursor:pointer;display:flex;align-items:center;justify-content:center;
  font-size:9px;color:var(--sap-navy);
}
.sap-wb:last-child{background:linear-gradient(180deg,#F4A0A0,#E06060);color:white;border-color:#C06060;}
/* Menu bar */
.sap-menubar{
  display:flex;align-items:center;padding:1px 6px;
  background:#FAFBFC;border-bottom:1px solid var(--sap-border);flex-shrink:0;
}
.sap-menu{
  padding:3px 10px;font-family:Arial,sans-serif;font-size:12px;
  color:var(--sap-navy);cursor:pointer;border-radius:2px;
  border:1px solid transparent;
}
.sap-menu:hover{background:#D8E8F4;border-color:#8BAFC5;}
/* Toolbar */
.sap-toolbar{
  display:flex;align-items:center;gap:2px;
  padding:4px 8px;background:white;
  border-bottom:1px solid var(--sap-border);flex-shrink:0;
}
.sap-tbn{
  width:24px;height:22px;border:1px solid transparent;border-radius:2px;
  display:flex;align-items:center;justify-content:center;cursor:pointer;
  font-size:13px;color:#555;background:transparent;
}
.sap-tbn:hover{background:#D8E8F4;border-color:#8BAFC5;}
.sap-sep{width:1px;height:18px;background:#B0C8D8;margin:0 3px;}
.sap-gi-btn{
  padding:2px 10px;background:#EEF8FF;border:1px solid var(--sap-blue);
  border-radius:2px;font-family:Arial,sans-serif;font-size:12px;
  font-weight:700;color:var(--sap-blue);cursor:pointer;
}
.sap-gi-btn:hover{background:#D0E8F8;}
/* Command / document bar */
.sap-cmdbar{
  display:flex;align-items:center;gap:8px;
  padding:5px 10px;background:white;
  border-bottom:1px solid var(--sap-border);flex-shrink:0;
}
.sap-cmdf{
  display:flex;align-items:center;
  border:1px solid #8BAFC5;border-radius:2px;overflow:hidden;background:white;
}
.sap-cmd-icon{
  width:24px;height:26px;background:#EEF4FA;
  border-right:1px solid #8BAFC5;display:flex;align-items:center;
  justify-content:center;font-size:12px;flex-shrink:0;
}
.sap-cmd-input{
  padding:3px 8px;font-family:"Courier New",monospace;
  font-size:12px;color:#333;background:white;
  border:none;outline:none;min-width:220px;
}
.sap-enter-btn{
  padding:3px 12px;background:linear-gradient(180deg,#F0F4F8,#D8E4EE);
  border:1px solid #8BAFC5;border-left:none;
  font-family:Arial,sans-serif;font-size:12px;color:var(--sap-navy);
  cursor:pointer;white-space:nowrap;
}
.sap-enter-btn:hover{background:linear-gradient(180deg,#E4EEF8,#C8D8E8);}
.sap-save-btn{
  display:flex;align-items:center;gap:5px;
  padding:3px 12px;background:linear-gradient(180deg,#F0F4F8,#D8E4EE);
  border:1px solid #8BAFC5;border-radius:2px;
  font-family:Arial,sans-serif;font-size:12px;color:var(--sap-navy);cursor:pointer;
}
.sap-save-btn:hover{background:linear-gradient(180deg,#E4EEF8,#C8D8E8);}
.sap-pgi-btn{
  display:flex;align-items:center;gap:6px;
  padding:4px 14px;
  background:linear-gradient(180deg,#FF9040,#F06800);
  border:1px solid #C05000;border-radius:2px;
  color:white;font-family:Arial,sans-serif;font-size:12px;
  font-weight:700;cursor:pointer;
}
.sap-pgi-btn:hover:not(:disabled){background:linear-gradient(180deg,#FFA050,#F07800);}
.sap-pgi-btn:disabled{opacity:.45;cursor:default;}
.sap-trx-select{
  padding:3px 8px;border:1px solid #8BAFC5;border-radius:2px;
  font-size:11.5px;font-family:Arial,sans-serif;color:var(--sap-navy);
  background:#EEF4FA;cursor:pointer;outline:none;margin-left:auto;
}
/* Form / header fields */
.sap-form{
  padding:8px 12px 6px;background:white;
  border-bottom:1px solid var(--sap-border);flex-shrink:0;
}
.sap-fr{display:flex;align-items:flex-end;gap:16px;flex-wrap:wrap;}
.sap-fg{display:flex;flex-direction:column;gap:2px;}
.sap-fl{font-size:10px;color:#555;font-family:Arial,sans-serif;white-space:nowrap;}
.sap-fi{
  padding:3px 6px;background:white;
  border:1px solid #8BAFC5;border-radius:1px;
  font-family:"Courier New",monospace;font-size:12px;
  color:#111;outline:none;
}
.sap-fn{
  padding:3px 8px;background:#F8FAFC;
  border:1px solid #8BAFC5;border-left:none;
  font-family:Arial,sans-serif;font-size:12px;color:#333;
  min-width:120px;
}
/* Sales area section */
.sap-section{
  padding:4px 12px;background:#EEF4FA;
  border-bottom:1px solid var(--sap-border);
  border-top:1px solid var(--sap-border);
  font-size:11px;font-weight:700;color:var(--sap-navy);
  font-family:Arial,sans-serif;letter-spacing:.5px;text-transform:uppercase;
  flex-shrink:0;
}
/* Tab bar */
.sap-tabbar{
  display:flex;align-items:flex-end;
  padding:0 12px;background:#F5F7FA;
  border-bottom:2px solid var(--sap-border);flex-shrink:0;
}
.sap-tab{
  padding:6px 16px;font-family:Arial,sans-serif;font-size:12.5px;
  color:#555;cursor:pointer;border:1px solid transparent;
  border-bottom:none;margin-bottom:-2px;background:transparent;
  white-space:nowrap;
}
.sap-tab:hover{background:#E4EEF8;color:var(--sap-navy);}
.sap-tab.active{
  background:white;color:var(--sap-navy);font-weight:700;
  border:1px solid var(--sap-border);border-bottom:2px solid white;
  border-radius:3px 3px 0 0;
}
/* Tab content */
.sap-tc{display:none;flex:1;overflow:hidden;flex-direction:column;}
.sap-tc.active{display:flex;}
.sap-tw{flex:1;overflow:auto;background:white;}
/* Tables */
.sap-tbl-t{width:100%;border-collapse:collapse;font-family:Arial,sans-serif;font-size:12px;}
.sap-tbl-t th{
  padding:5px 10px;
  background:linear-gradient(180deg,#D8E8F4,#C4D8EC);
  border:1px solid #A8C0D4;
  color:var(--sap-navy);font-weight:700;text-align:left;
  white-space:nowrap;font-size:11.5px;position:sticky;top:0;z-index:2;
}
.sap-tbl-t td{
  padding:4px 10px;
  border:1px solid #D8E8F4;
  color:#111;white-space:nowrap;font-size:12px;
}
.sap-tbl-t tr:nth-child(even) td{background:#F4F8FC;}
.sap-tbl-t tr:hover td{background:#E0EEFA;}
.sap-link{color:var(--sap-blue);text-decoration:underline;cursor:pointer;}
.sap-link:hover{color:#0050AA;}
/* Status bar */
.sap-statusbar{
  display:flex;align-items:center;gap:8px;
  padding:4px 10px;background:#EEF2F6;
  border-top:1px solid var(--sap-border);
  min-height:28px;flex-shrink:0;
}
.sap-st-icon{
  width:18px;height:18px;border-radius:3px;
  display:flex;align-items:center;justify-content:center;
  font-size:11px;font-weight:700;color:white;flex-shrink:0;
}
.sap-st-ok{background:#22C55E;}
.sap-st-warn{background:#F59E0B;}
.sap-st-txt{font-family:Arial,sans-serif;font-size:12px;color:#333;}
/* Info banner */
.sap-info-bar{
  display:flex;align-items:center;gap:8px;
  padding:5px 12px;background:#FFF7ED;
  border-bottom:1px solid #FED7AA;flex-shrink:0;
}
.sap-info-txt{font-family:Arial,sans-serif;font-size:11.5px;color:var(--sap-amber);font-weight:500;}

/* ── OTC Stepper ── */
.otc-stepper{display:flex;align-items:flex-start;padding:18px 24px;background:#F8FAFC;border-radius:14px;border:1px solid var(--border);margin:14px 0;}
.otc-step{display:flex;flex-direction:column;align-items:center;flex:1;position:relative;}
.otc-step:not(:last-child)::after{content:'';position:absolute;top:20px;left:50%;width:100%;height:2px;background:var(--border);z-index:0;}
.otc-step.done::after{background:#22C55E;}
.otc-step.active::after{background:linear-gradient(to right,#22C55E,var(--border));}
.otc-step-circle{width:40px;height:40px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;z-index:1;border:2.5px solid var(--border);background:white;color:var(--sub);}
.otc-step.done .otc-step-circle{background:#22C55E;border-color:#22C55E;color:white;}
.otc-step.active .otc-step-circle{background:var(--orange);border-color:var(--orange);color:white;animation:pulse-ring 1.6s ease-in-out infinite;}
.otc-step-label{font-size:10px;font-weight:600;color:var(--sub);margin-top:8px;text-align:center;line-height:1.3;max-width:72px;}
.otc-step.done .otc-step-label{color:#15803D;}
.otc-step.active .otc-step-label{color:var(--orange);font-weight:800;}
@keyframes pulse-ring{0%,100%{box-shadow:0 0 0 0 rgba(249,115,22,.4);}50%{box-shadow:0 0 0 8px rgba(249,115,22,0);}}
.email-meta-row{display:flex;align-items:center;gap:8px;font-size:12.5px;color:var(--sub);flex-wrap:wrap;padding:4px 0;}
.email-oc-badge{padding:3px 12px;border-radius:20px;border:1.5px solid #3B7DC8;background:#EEF4FF;color:#1D4ED8;font-size:11.5px;font-weight:700;font-family:var(--mono);cursor:pointer;}
.email-oc-badge:hover{background:#3B7DC8;color:white;}
.email-section-lbl{font-size:10.5px;font-weight:800;color:var(--sub);letter-spacing:.9px;text-transform:uppercase;padding:12px 20px 6px;border-top:1px solid var(--border);display:flex;align-items:center;gap:6px;}
/* Detail modal */
.det-modal{max-width:680px;width:95vw;}
.det-grid{display:grid;grid-template-columns:1fr 1fr;border:1px solid var(--border);border-radius:12px;overflow:hidden;}
.det-cell{padding:12px 16px;border-bottom:1px solid var(--border);}
.det-cell:nth-last-child(-n+2){border-bottom:none;}
.det-lbl{font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.7px;text-transform:uppercase;margin-bottom:3px;}
.det-val{font-size:13.5px;font-weight:600;color:var(--text);}
.det-val.mono{font-family:var(--mono);font-size:12.5px;}
.det-val.blue{color:#2563EB;cursor:pointer;}
.det-val.big{font-size:15px;font-weight:800;color:var(--orange);}
.det-items-tbl{width:100%;border-collapse:collapse;font-size:12.5px;}
.det-items-tbl th{background:#F1F5F9;padding:9px 12px;text-align:left;font-size:10px;font-weight:800;color:var(--sub);letter-spacing:.7px;text-transform:uppercase;}
.det-items-tbl td{padding:11px 12px;border-top:1px solid var(--border);vertical-align:middle;}
.det-items-tbl td.sku{font-family:var(--mono);font-size:11.5px;color:#2563EB;font-weight:600;}
.det-items-tbl td.qty{font-weight:700;}
.det-items-tbl td.tot{font-weight:800;}
.det-items-tbl tr:hover td{background:#F8FAFC;}
.sap-chk{display:flex;align-items:center;gap:10px;padding:11px 14px;border:1px solid #D1FAE5;border-radius:10px;background:#F0FDF4;margin-bottom:8px;}
.sap-chk.fail{border-color:#FEE2E2;background:#FFF5F5;}
.sap-chk-ico{width:22px;height:22px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:12px;flex-shrink:0;}
.sap-chk-ico.ok{background:#22C55E;color:white;}
.sap-chk-ico.fail{background:#EF4444;color:white;}
/* Warn modal */
.warn-det{max-width:560px;width:95vw;}
.warn-det-hd{padding:18px 22px;border-bottom:1px solid var(--border);}
.warn-alert{margin:14px 20px;padding:14px 16px;background:#FFF1F0;border:1.5px solid #FCA5A5;border-radius:12px;}
.warn-alert-ttl{font-size:13px;font-weight:800;color:#DC2626;display:flex;align-items:center;gap:7px;margin-bottom:6px;}
.warn-alert-body{font-size:12.5px;color:#7F1D1D;line-height:1.6;}
.warn-sol-lbl{font-size:11px;font-weight:800;color:var(--sub);letter-spacing:.7px;padding:4px 20px 8px;text-transform:uppercase;}
.warn-ropt{display:flex;align-items:flex-start;gap:12px;padding:14px 20px;cursor:pointer;border-bottom:1px solid var(--border);transition:background .15s;}
.warn-ropt:last-child{border-bottom:none;}
.warn-ropt:hover,.warn-ropt.sel{background:#FFF7ED;}
.warn-radio{width:20px;height:20px;border-radius:50%;border:2px solid var(--border);display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:2px;}
.warn-ropt.sel .warn-radio{border-color:var(--orange);}
.warn-radio-dot{width:10px;height:10px;border-radius:50%;background:var(--orange);display:none;}
.warn-ropt.sel .warn-radio-dot{display:block;}
.warn-rlbl{font-size:13.5px;font-weight:700;color:var(--text);margin-bottom:3px;}
.warn-rdesc{font-size:12px;color:var(--sub);line-height:1.4;}

</style>
</head>
<body>

<!-- ══════════ SIDEBAR ══════════ -->
<nav class="sidebar">
  <div class="sidebar-logo">
    <div class="logo-wrap">
      <div class="logo-icon">C</div>
      <div style="line-height:1.2;">
        <div class="logo-main">Caffenio <span>Ops</span></div>
        <div class="logo-sub">SAP Automation Hub</div>
      </div>
    </div>
  </div>
  <div class="sidebar-nav">
    <div class="nav-section" style="margin-top:6px;">Principal</div>
    <div class="nav-item" onclick="navigate('email-inbox')" id="nav-email-inbox">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
      Email Inbox
    </div>
    <div class="nav-item active" onclick="navigate('lifecycle')" id="nav-lifecycle">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg>
      Lifecycle Dashboard <span class="nav-dot"></span>
    </div>
    <div class="nav-item" onclick="navigate('control-tower')" id="nav-control-tower">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M12 1v4M12 19v4M4.22 4.22l2.83 2.83M16.95 16.95l2.83 2.83M1 12h4M19 12h4M4.22 19.78l2.83-2.83M16.95 7.05l2.83-2.83"/></svg>
      AI Control Tower
    </div>
    <div class="nav-section" style="margin-top:6px;">SAP Sales &amp; Dist.</div>
    <div class="nav-item" onclick="navigate('sap-va01')" id="nav-sap-va01">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14,2 14,8 20,8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/></svg>
      VA01 – Sales Orders
    </div>
    <div class="nav-item" onclick="navigate('sap-vl01n')" id="nav-sap-vl01n">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="1 4 1 10 7 10"/><path d="M3.51 15a9 9 0 1 0 .49-4.5"/></svg>
      VL01N – Check Deliv.
    </div>
    <div class="nav-item" onclick="navigate('sap-vl02n')" id="nav-sap-vl02n">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="5 3 19 12 5 21 5 3"/></svg>
      VL02N – PGI Dispatch
    </div>
    <div class="nav-section" style="margin-top:6px;">Inteligencia IA</div>
    <div class="nav-item" onclick="navigate('agent-observatory')" id="nav-agent-observatory">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="4"/><path d="M1.05 12H7M17 12h5.95M12 1.05V7m0 10v5.95M4.22 4.22l4.24 4.24M15.54 15.54l4.24 4.24M19.78 4.22l-4.24 4.24M8.46 15.54l-4.24 4.24"/></svg>
      Monitor de Agentes
    </div>
    <div class="nav-item" onclick="navigate('business-rules')" id="nav-business-rules">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
      Reglas de Negocio
    </div>
  </div>
  <div class="sidebar-footer">
    <div class="supabase-badge">
      <span class="pulse-dot"></span>
      <div style="font-size:9px;">
        <div style="font-weight:600;color:rgba(255,255,255,.4);">SUPABASE SYNC</div>
        <div style="color:rgba(255,255,255,.25);">Region: mx-central-1</div>
      </div>
    </div>
  </div>
</nav>

<!-- ══════════ MAIN ══════════ -->
<div class="main">
  <div class="topbar">
    <div class="topbar-title" id="topbar-title">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" width="18" height="18"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg>
      Lifecycle Dashboard
    </div>
    <button class="btn btn-dark" onclick="syncEmail()">
      <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
      Sync Email
    </button>
    <button class="btn btn-orange">
      <svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 14.5v-9l6 4.5-6 4.5z"/></svg>
      Voice Order
    </button>
    <button class="btn btn-ghost" style="padding:7px 9px;" onclick="syncEmail()">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="1 4 1 10 7 10"/><polyline points="23 20 23 14 17 14"/><path d="M20.49 9A9 9 0 0 0 5.64 5.64L1 10m22 4l-4.64 4.36A9 9 0 0 1 3.51 15"/></svg>
    </button>
    <div class="daemon-badge"><span class="daemon-dot-off" id="daemon-dot"></span><span id="daemon-status">DAEMON: OFFLINE</span></div>
    <div class="agents-online"><span class="pulse-dot"></span>Agents Online: 7/12</div>
    <div class="user-badge"><div class="user-avatar">RG</div>Rommel Gil</div>
  </div>

  <div class="content">

    <!-- ════ LIFECYCLE ════ -->
    <div class="view active" id="view-lifecycle">
      <!-- Header -->
      <div style="display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:16px;flex-wrap:wrap;gap:10px;">
        <div>
          <h2 style="font-size:18px;font-weight:800;color:var(--text);display:flex;align-items:center;gap:8px;">
            📦 Lifecycle de Pedidos
            <span style="font-size:12px;font-weight:500;color:var(--sub);background:var(--light);padding:3px 10px;border-radius:20px;border:1px solid var(--border);">— 10 días</span>
          </h2>
          <div style="font-size:12px;color:var(--sub);margin-top:3px;">21–30 Abr 2026 · Base de operación: <strong>~4,100 pedidos/mes</strong></div>
        </div>
        <div style="display:flex;gap:8px;align-items:center;">
          <input class="lc-search" placeholder="🔍 Buscar tienda, SAP Order, SKU…" id="lc-search-input" oninput="setLCSearch(this.value)" style="width:260px;">
          <button class="btn btn-orange" style="font-size:12px;padding:7px 16px;font-weight:700;" onclick="processAll()">✦ Process All Pending</button>
        </div>
      </div>

      <!-- Filter bar: Todos pill + Día picker + Mes selector -->
      <div class="lc-filter-bar" id="lc-filter-bar">
        <button class="lc-pill active" id="lc-pill-all" onclick="setLCFilterAll()">
          📋 Todos <span class="lc-pill-count" id="lc-pill-count">—</span>
        </button>
        <div style="display:flex;align-items:center;gap:6px;">
          <span style="font-size:12px;color:var(--sub);font-weight:600;">📅 Día:</span>
          <input type="date" class="lc-date-input" id="lc-day-input" onchange="setLCDayFilter(this.value)">
        </div>
        <div style="display:flex;align-items:center;gap:6px;">
          <span style="font-size:12px;color:var(--sub);font-weight:600;">Mes:</span>
          <select class="lc-month-sel" id="lc-month-sel" onchange="setLCMonthFilter(this.value)">
            <option value="">Todos</option>
            <option value="04">Abril 2026</option>
            <option value="03">Marzo 2026</option>
            <option value="05">Mayo 2026</option>
          </select>
        </div>
      </div>

      <!-- 4 KPI cards -->
      <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:20px;">
        <div class="metric-card" id="kpi-all" style="cursor:pointer;border:2px solid var(--orange);">
          <div><div class="metric-label">ALL (TODOS)</div><div class="metric-val" id="cnt-all" style="color:var(--orange);">—</div></div>
          <div class="metric-icon" style="background:#FFF7ED;"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#F97316" stroke-width="2"><rect x="3" y="3" width="7" height="7" rx="1"/><rect x="14" y="3" width="7" height="7" rx="1"/><rect x="3" y="14" width="7" height="7" rx="1"/><rect x="14" y="14" width="7" height="7" rx="1"/></svg></div>
        </div>
        <div class="metric-card"><div><div class="metric-label">BACKLOG (PENDIENTES)</div><div class="metric-val" id="cnt-backlog">—</div></div><div class="metric-icon mic-orange"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#F97316" stroke-width="2"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg></div></div>
        <div class="metric-card"><div><div class="metric-label">PROCESSED (SUCCESS)</div><div class="metric-val" id="cnt-success">—</div></div><div class="metric-icon mic-green"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#22C55E" stroke-width="2"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22,4 12,14.01 9,11.01"/></svg></div></div>
        <div class="metric-card"><div><div class="metric-label">ERRORS (FALLIDOS)</div><div class="metric-val" id="cnt-errors">—</div></div><div class="metric-icon mic-red"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#EF4444" stroke-width="2"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="12"/><line x1="12" y1="16" x2="12.01" y2="16"/></svg></div></div>
      </div>

      <!-- Table card -->
      <div class="lifecycle-card">
        <div class="tabs">
          <div class="tab active" id="tab-backlog" onclick="switchTab('backlog')">Backlog <span class="tab-count" id="tc-backlog">—</span></div>
          <div class="tab" id="tab-success" onclick="switchTab('success')">Success <span class="tab-count" id="tc-success">—</span></div>
          <div class="tab" id="tab-errors" onclick="switchTab('errors')">Errors <span class="tab-count" id="tc-errors">—</span></div>
          <div class="tab-spacer"></div>
          <button class="btn btn-orange" style="font-size:11.5px;padding:5px 14px;font-weight:700;" onclick="processAll()">Process All</button>
        </div>
        <div id="panel-backlog">
          <div class="table-header grid-backlog">
            <span></span><span>Tienda / Fecha</span><span>Recibido</span><span>Resumen</span><span>Estado</span><span>Acciones</span>
          </div>
          <div id="backlog-rows"></div>
        </div>
        <div id="panel-success" style="display:none;">
          <div class="table-header grid-success">
            <span></span><span>Tienda / Fecha</span><span>Recibido</span><span>Resumen</span><span>Estado</span><span>SAP SD Order</span><span>Acciones</span>
          </div>
          <div id="success-rows"></div>
        </div>
        <div id="panel-errors" style="display:none;">
          <div class="table-header grid-errors">
            <span></span><span>Tienda / Fecha</span><span>Recibido</span><span>Resumen</span><span>Estado / Error</span><span>SAP SD Order</span><span>Acciones</span>
          </div>
          <div id="errors-rows"></div>
        </div>
        <div id="lc-pagination"></div>
      </div>
    </div>

    <!-- ════ WARN CORRECTION MODAL ════ -->
    <div class="modal-overlay" id="modal-warn-correction"><div class="modal warn-det" style="padding:0;overflow:hidden;"><div class="warn-det-hd"><div style="display:flex;align-items:flex-start;justify-content:space-between;"><div><div style="font-size:17px;font-weight:800;color:var(--text);display:flex;align-items:center;gap:8px;"><span>⚠</span><span id="warn-modal-title-txt">Advertencia</span></div><div style="font-size:12px;color:var(--sub);margin-top:3px;" id="warn-modal-sub">Diagnóstico Agente IA</div></div><button class="modal-close" onclick="closeModal('modal-warn-correction')">✕</button></div></div><div id="warn-alert-area"></div><div class="warn-sol-lbl">🤖 Soluciones sugeridas:</div><div id="warn-options-container" style="border-top:1px solid var(--border);border-bottom:1px solid var(--border);"></div><div style="padding:16px 20px;display:flex;justify-content:flex-end;gap:10px;"><button class="btn btn-ghost" style="padding:8px 18px;" onclick="closeModal('modal-warn-correction')">Cancelar</button><button class="btn btn-orange" id="warn-apply-btn" onclick="applyWarnCorrection()" disabled style="opacity:.5;padding:8px 20px;font-size:13px;"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polygon points="5 3 19 12 5 21 5 3"/></svg> Aplicar Corrección</button></div></div></div>

    <!-- ════ EMAIL INBOX ════ -->
    <div class="view" id="view-email-inbox">
      <div class="inbox-layout">
        <div class="email-list-panel">
          <div class="email-list-header"><div style="font-size:13px;font-weight:700;">📬 Bandeja de Entrada OC</div><span class="badge badge-pending">6 Sin leer</span></div>
          <input class="email-search" placeholder="🔍 Buscar correos..." id="email-search" oninput="filterEmails(this.value)">
          <div class="email-list-body" id="email-list-body"></div>
        </div>
        <div class="email-detail-panel" id="email-detail-content">
          <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;height:100%;padding:60px;color:var(--sub);gap:12px;">
            <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" opacity="0.3"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
            <div style="font-size:13px;text-align:center;">Selecciona un correo para ver el detalle y el análisis IA</div>
          </div>
        </div>
      </div>
    </div>

    <!-- ════ AI CONTROL TOWER ════ -->
    <div class="view" id="view-control-tower">
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:16px;flex-wrap:wrap;">
        <div style="display:flex;align-items:center;gap:7px;background:white;padding:7px 14px;border-radius:20px;border:1px solid var(--border);font-size:11.5px;font-weight:600;"><span class="pulse-dot"></span>SYSTEM PULSE: 142MS</div>
        <button class="btn btn-dark" style="font-size:11.5px;" onclick="runBottleneck()"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="1 4 1 10 7 10"/><path d="M3.51 15a9 9 0 1 0 .49-4.5"/></svg>Run AI Bottleneck Analysis</button>
      </div>

      <!-- Row 1: Volúmenes Procesados (Image 3 style) -->
      <div class="ct-card ct-card-wide" style="margin-bottom:14px;">
        <div class="ct-header" style="margin-bottom:14px;">
          <div><div class="ct-title">📊 Volúmenes Procesados</div><div class="ct-subtitle">PEDIDOS CORRECTOS POR FECHA DE LLEGADA · CLICK EN BARRA = FILTRAR LIFECYCLE</div></div>
          <div id="ct-proc-stats" style="display:flex;gap:10px;"></div>
        </div>
        <div style="display:flex;align-items:flex-end;gap:6px;height:140px;" id="ct-proc-chart"></div>
        <div style="display:flex;gap:0;margin-top:4px;" id="ct-proc-labels"></div>
      </div>

      <!-- Row 2: Two charts side by side -->
      <div class="ct-layout" style="margin-bottom:14px;">
        <!-- Aging chart -->
        <div class="ct-card">
          <div class="ct-header" style="margin-bottom:14px;">
            <div><div class="ct-title">⏳ Aging de Pendientes + Errores</div><div class="ct-subtitle">TIEMPO DESDE LLEGADA HASTA HOY</div></div>
          </div>
          <div id="ct-aging-chart"></div>
          <div id="ct-aging-stats" style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-top:12px;"></div>
        </div>
        <!-- By client type -->
        <div class="ct-card">
          <div class="ct-header" style="margin-bottom:14px;">
            <div><div class="ct-title">🏪 Por Tipo de Cliente / Área</div><div class="ct-subtitle">DISTRIBUCIÓN DE PEDIDOS OXXO</div></div>
          </div>
          <div id="ct-client-chart"></div>
        </div>
      </div>

      <!-- Row 3: Top Materials + Stock -->
      <div class="ct-card ct-card-wide" style="margin-bottom:14px;">
        <div class="ct-header" style="margin-bottom:14px;">
          <div><div class="ct-title">📦 Top Materiales Caffenio</div><div class="ct-subtitle">FRECUENCIA DE PEDIDO VS STOCK DISPONIBLE ESTIMADO</div></div>
          <div style="display:flex;gap:12px;"><div style="display:flex;align-items:center;gap:6px;font-size:11.5px;color:rgba(255,255,255,.6);"><div style="width:12px;height:12px;border-radius:3px;background:var(--teal);"></div>Pedidos (líneas)</div><div style="display:flex;align-items:center;gap:6px;font-size:11.5px;color:rgba(255,255,255,.6);"><div style="width:12px;height:12px;border-radius:3px;background:rgba(249,115,22,.7);"></div>Stock disponible</div></div>
        </div>
        <div id="ct-materials-chart"></div>
      </div>

      <!-- Row 4: SLA Performance -->
      <div class="ct-card ct-card-wide">
        <div class="ct-header" style="margin-bottom:14px;">
          <div><div class="ct-title"><span style="background:var(--orange);width:32px;height:32px;border-radius:10px;display:flex;align-items:center;justify-content:center;">⚡</span>SLA Performance Report</div><div class="ct-subtitle">AI CONTROL TOWER · CAFFENIO OTC</div></div>
          <button class="ct-btn" onclick="runBottleneck()">Run AI Bottleneck Analysis</button>
        </div>
        <div id="ct-sla-content"></div>
      </div>
    </div>


    <!-- ════ MODULE 5: AGENT OBSERVATORY ════ -->
    <div class="view" id="view-agent-observatory">
      <div class="obs-layout">
        <!-- Left agent list -->
        <div class="obs-sidebar">
          <div class="obs-sidebar-header">
            <input class="obs-search" placeholder="🔍 Search agents..." id="obs-search" oninput="filterAgents(this.value)">
          </div>
          <div class="obs-agent-list" id="obs-agent-list"></div>
        </div>
        <!-- Right detail -->
        <div class="obs-main" id="obs-main"></div>
      </div>
    </div>

    <!-- ════ MODULE 6: BUSINESS RULES ════ -->
    <div class="view" id="view-business-rules">
      <div style="display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:20px;gap:16px;flex-wrap:wrap;">
        <div>
          <h2 style="font-size:26px;font-weight:800;color:var(--text);margin-bottom:4px;">Admin Console</h2>
          <p style="font-size:13px;color:var(--sub);">Configuración del sistema, gobernanza de IA y políticas de aprobación.</p>
        </div>
        <div style="display:flex;gap:10px;">
          <button class="btn btn-ghost"><svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15,3 21,3 21,9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>Repository</button>
          <button class="btn btn-orange" onclick="showToast('✅ Cambios guardados exitosamente')"><svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg>Save Changes</button>
        </div>
      </div>
      <div class="admin-layout">
        <!-- AI Governance & Models -->
        <div class="admin-card">
          <div class="admin-card-header">
            <div class="admin-card-title"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M19.07 4.93A10 10 0 0 1 21 12a9.9 9.9 0 0 1-1.93 5.87M4.93 4.93A10 10 0 0 0 3 12a9.9 9.9 0 0 0 1.93 5.87"/></svg>AI Governance &amp; Models</div>
            <div class="admin-card-sub">Estado y versiones de los agentes activos del sistema</div>
          </div>
          <div id="admin-agents-list"></div>
        </div>
        <!-- Approval Policies -->
        <div class="admin-card">
          <div class="admin-card-header">
            <div class="admin-card-title"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>Approval Policies &amp; Thresholds</div>
            <div class="admin-card-sub">Reglas de negocio configurables y umbrales de aprobación</div>
          </div>
          <div id="admin-rules-list"></div>
          <div class="admin-add-rule" onclick="addNewRule()"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="16"/><line x1="8" y1="12" x2="16" y2="12"/></svg>Define New Approval Threshold</div>
        </div>
        <!-- Process Config -->
        <div class="admin-card" style="grid-column:1/-1;">
          <div class="admin-card-header">
            <div class="admin-card-title"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="3" width="20" height="14" rx="2"/><line x1="8" y1="21" x2="16" y2="21"/><line x1="12" y1="17" x2="12" y2="21"/></svg>Configuración de Proceso OTC</div>
            <div class="admin-card-sub">Parámetros operativos del flujo Order-to-Cash de Caffenio</div>
          </div>
          <div id="admin-process-config"></div>
        </div>
      </div>
    </div>

    <!-- ════ REPOSITORIO DE DOCUMENTOS ════ -->
    <div class="view" id="view-repositorio">
      <div class="repo-toolbar">
        <input class="repo-search" placeholder="Buscar documentos, POs, clientes…" id="repo-search-input" oninput="filterRepoDocs(this.value)">
        <select class="repo-filter" id="repo-filter-type" onchange="filterRepoDocs('')">
          <option value="all">Todos los tipos</option>
          <option value="xlsx">Excel (OC)</option>
          <option value="pdf">PDF</option>
          <option value="msg">MSG (Correo)</option>
        </select>
        <select class="repo-filter" id="repo-filter-status" onchange="filterRepoDocs('')">
          <option value="all">Todos los estados</option>
          <option value="proc">Procesados</option>
          <option value="pend">Pendientes</option>
        </select>
        <button class="btn btn-orange" onclick="showToast('📤 Subiendo nuevo documento…')">
          <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
          Subir Documento
        </button>
      </div>
      <div class="repo-stats">
        <div class="repo-stat-card"><div><div class="repo-stat-lbl">Total Documentos</div><div class="repo-stat-val">17</div></div><div style="width:40px;height:40px;background:#EFF6FF;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;">📁</div></div>
        <div class="repo-stat-card"><div><div class="repo-stat-lbl">Órdenes de Compra</div><div class="repo-stat-val">9</div></div><div style="width:40px;height:40px;background:#F0FDF4;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;">📊</div></div>
        <div class="repo-stat-card"><div><div class="repo-stat-lbl">PDFs</div><div class="repo-stat-val">6</div></div><div style="width:40px;height:40px;background:#FFF1F2;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;">📄</div></div>
        <div class="repo-stat-card"><div><div class="repo-stat-lbl">Procesados en SAP</div><div class="repo-stat-val">12</div></div><div style="width:40px;height:40px;background:#F0FDF4;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;">✅</div></div>
      </div>
      <div class="repo-grid" id="repo-grid"></div>
    </div>


    <!-- ════ SAP VA01 – SALES ORDERS ════ -->
    <div class="view" id="view-sap-va01">
      <div class="sap-wrap">
        <div class="sap-window">

          <!-- ── Title bar ── -->
          <div class="sap-titlebar">
            <div class="sap-titlebar-left">
              <div class="sap-win-icon" style="background:#EEF4FA;border:1px solid #8BAFC5;">📋</div>
              <span class="sap-win-title" id="va01-win-title">Display Sales Order: Overview — 100025255</span>
            </div>
            <div class="sap-wbtns">
              <div class="sap-wb">─</div><div class="sap-wb">□</div><div class="sap-wb">✕</div>
            </div>
          </div>

          <!-- ── Menu bar ── -->
          <div class="sap-menubar">
            <span class="sap-menu">Sales order</span>
            <span class="sap-menu">Edit</span>
            <span class="sap-menu">Goto</span>
            <span class="sap-menu">Extras</span>
            <span class="sap-menu">Environment</span>
            <span class="sap-menu">System</span>
            <span class="sap-menu">Help</span>
          </div>

          <!-- ── Toolbar ── -->
          <div class="sap-toolbar">
            <button class="sap-tbn" title="Back" onclick="navigate('lifecycle')">←</button>
            <button class="sap-tbn" title="Home">🏠</button>
            <button class="sap-tbn" title="Cancel">✕</button>
            <div class="sap-sep"></div>
            <button class="sap-tbn" title="Print">🖨</button>
            <button class="sap-tbn" title="Find">🔍</button>
            <div class="sap-sep"></div>
            <button class="sap-tbn" title="Prev">◄</button>
            <button class="sap-tbn" title="Next">►</button>
            <div class="sap-sep"></div>
            <button class="sap-tbn" title="Edit" style="color:var(--sap-amber);">✏</button>
            <div style="flex:1;"></div>
            <select class="sap-trx-select" onchange="navigate(this.value);this.value='sap-va01'">
              <option value="sap-va01" selected>VA01/VA03 – Sales Orders</option>
              <option value="sap-vl01n">VL01N – Check Delivery</option>
              <option value="sap-vl02n">VL02N – PGI Dispatch</option>
            </select>
          </div>

          <!-- ── Command bar ── -->
          <div class="sap-cmdbar">
            <div class="sap-cmdf">
              <div class="sap-cmd-icon">🔍</div>
              <input class="sap-cmd-input" id="va01-doc-input" style="width:200px;" readonly>
            </div>
            <button class="sap-enter-btn">Enter</button>
            <button class="sap-save-btn" onclick="showToast('💾 Documento guardado')">
              <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg>
              Save
            </button>
            <div style="flex:1;"></div>
            <select class="sap-trx-select" onchange="populateSap(this.value)" id="va01-order-selector">
              <option value="s001">SO 100025255 · OXXO Reforma</option>
              <option value="s002">SO 100057527 · OXXO Insurgentes</option>
              <option value="s003">SO 100034317 · OXXO Santa María</option>
              <option value="s004">SO 100017625 · OXXO Lerma</option>
              <option value="s005">SO 100058448 · OXXO Lerma 2</option>
            </select>
          </div>

          <!-- ── Header fields ── -->
          <div class="sap-form">
            <div class="sap-fr">
              <div class="sap-fg">
                <div class="sap-fl">Standard Order</div>
                <input class="sap-fi" id="va01-order-num" style="width:95px;" readonly>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">Sold-To Party</div>
                <div style="display:flex;">
                  <input class="sap-fi" id="va01-soldto-id" style="width:62px;" readonly>
                  <span class="sap-fn" id="va01-soldto-name" style="min-width:200px;"></span>
                </div>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">Ship-To Party</div>
                <div style="display:flex;">
                  <input class="sap-fi" id="va01-sh-id" style="width:62px;" readonly>
                  <span class="sap-fn" id="va01-sh-name" style="min-width:160px;"></span>
                </div>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">PO Number</div>
                <input class="sap-fi" id="va01-po-num" style="width:140px;" readonly>
              </div>
            </div>
          </div>

          <!-- ── Tab bar ── -->
          <div class="sap-tabbar" id="va01-tabbar">
            <div class="sap-tab active" onclick="switchSapTab('va01','sales',this)">Sales</div>
            <div class="sap-tab" onclick="switchSapTab('va01','itemov',this)">Item overview</div>
            <div class="sap-tab" onclick="switchSapTab('va01','ordering',this)">Ordering party</div>
            <div class="sap-tab" onclick="switchSapTab('va01','shipping',this)">Shipping</div>
            <div class="sap-tab" onclick="switchSapTab('va01','rejection',this)">Reason for rej.</div>
          </div>

          <!-- ── Tab: Sales ── -->
          <div class="sap-tc active" id="va01-tab-sales">
            <div style="flex:1;overflow:auto;background:white;">
              <!-- Sales Area section -->
              <div class="sap-section">Sales Area</div>
              <div class="sap-form" style="border-bottom:none;">
                <div class="sap-fr">
                  <div class="sap-fg">
                    <div class="sap-fl">Sales Org. / Distr.Ch. / Division</div>
                    <div style="display:flex;gap:4px;">
                      <input class="sap-fi" value="CAF1" style="width:50px;" readonly>
                      <input class="sap-fi" value="10" style="width:34px;" readonly>
                      <input class="sap-fi" value="00" style="width:34px;" readonly>
                    </div>
                  </div>
                  <div class="sap-fg">
                    <div class="sap-fl">Net Value</div>
                    <div style="display:flex;align-items:center;gap:4px;">
                      <input class="sap-fi" id="va01-net-val" style="width:100px;text-align:right;" readonly>
                      <span style="font-family:Arial;font-size:12px;color:#555;">MXN</span>
                    </div>
                  </div>
                  <div class="sap-fg">
                    <div class="sap-fl">Order Date</div>
                    <input class="sap-fi" id="va01-order-date" style="width:88px;" readonly>
                  </div>
                  <div class="sap-fg">
                    <div class="sap-fl">Req. Deliv. Date</div>
                    <input class="sap-fi" id="va01-deliv-date" style="width:88px;" readonly>
                  </div>
                </div>
              </div>
              <!-- Items table -->
              <table class="sap-tbl-t">
                <thead>
                  <tr>
                    <th style="width:55px;">Item</th>
                    <th style="width:110px;">Material</th>
                    <th>Description</th>
                    <th style="width:85px;text-align:right;">Order Qty</th>
                    <th style="width:40px;">Un</th>
                    <th style="width:90px;text-align:right;">Net Price</th>
                    <th style="width:60px;">Plant</th>
                    <th style="width:90px;">Deliv. Date</th>
                    <th style="width:80px;">Status</th>
                  </tr>
                </thead>
                <tbody id="va01-tbody"></tbody>
              </table>
            </div>
          </div>

          <!-- ── Tab: Item overview ── -->
          <div class="sap-tc" id="va01-tab-itemov">
            <div style="flex:1;overflow:auto;background:white;">
              <table class="sap-tbl-t">
                <thead>
                  <tr>
                    <th style="width:55px;">Item</th>
                    <th style="width:110px;">Material</th>
                    <th>Description</th>
                    <th style="width:85px;text-align:right;">Order Qty</th>
                    <th style="width:40px;">Un</th>
                    <th style="width:85px;text-align:right;">Conf.Qty</th>
                    <th style="width:90px;text-align:right;">Net Price</th>
                    <th style="width:80px;">Status</th>
                  </tr>
                </thead>
                <tbody id="va01-item-ov-tbody"></tbody>
              </table>
            </div>
          </div>

          <!-- ── Tab: Ordering party ── -->
          <div class="sap-tc" id="va01-tab-ordering">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-form" style="border-bottom:none;">
                <div style="display:flex;flex-direction:column;gap:10px;">
                  <div class="sap-fg"><div class="sap-fl">Sold-To Party</div><div style="display:flex;"><input class="sap-fi" id="va01-op-soldto" style="width:340px;" readonly></div></div>
                  <div class="sap-fg"><div class="sap-fl">Ship-To Party</div><div style="display:flex;"><input class="sap-fi" id="va01-op-shipto" style="width:340px;" readonly></div></div>
                  <div class="sap-fg"><div class="sap-fl">Payer</div><div style="display:flex;"><input class="sap-fi" id="va01-op-payer" style="width:340px;" readonly></div></div>
                  <div class="sap-fg"><div class="sap-fl">Customer Ref.</div><div style="display:flex;"><input class="sap-fi" id="va01-op-ref" style="width:220px;" readonly></div></div>
                </div>
              </div>
            </div>
          </div>

          <!-- ── Tab: Shipping ── -->
          <div class="sap-tc" id="va01-tab-shipping">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-form" style="border-bottom:none;">
                <div class="sap-fr">
                  <div class="sap-fg"><div class="sap-fl">Shipping Conditions</div><input class="sap-fi" value="01 — Standard" style="width:160px;" readonly></div>
                  <div class="sap-fg"><div class="sap-fl">Delivery Priority</div><input class="sap-fi" value="02 — Normal" style="width:120px;" readonly></div>
                  <div class="sap-fg"><div class="sap-fl">Shipping Date</div><input class="sap-fi" id="va01-sh-date" style="width:88px;" readonly></div>
                </div>
              </div>
            </div>
          </div>

          <!-- ── Tab: Rejection ── -->
          <div class="sap-tc" id="va01-tab-rejection">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-form" style="border-bottom:none;">
                <div style="font-family:Arial;font-size:12px;color:#555;padding:8px 0;">No rejection reasons assigned to this sales order.</div>
              </div>
            </div>
          </div>

          <!-- ── Status bar ── -->
          <div class="sap-statusbar">
            <div class="sap-st-icon sap-st-ok">S</div>
            <span class="sap-st-txt" id="va01-status-text">Display Sales Order — SAP System: CAF1</span>
            <div style="flex:1;"></div>
            <span style="font-size:10.5px;font-family:Arial;color:#666;">Client: CAF | User: JPALAO | T-Code: VA03</span>
          </div>

        </div>
      </div>
    </div>

    <!-- ════ SAP VL01N – CHECK DELIVERY ════ -->
    <div class="view" id="view-sap-vl01n">
      <div class="sap-wrap">
        <div class="sap-window">

          <div class="sap-titlebar">
            <div class="sap-titlebar-left">
              <div class="sap-win-icon" style="background:#E8F8E8;border:1px solid #6BBF6B;">🔄</div>
              <span class="sap-win-title">Display Outbound Delivery: Overview — VL03N</span>
            </div>
            <div class="sap-wbtns"><div class="sap-wb">─</div><div class="sap-wb">□</div><div class="sap-wb">✕</div></div>
          </div>

          <div class="sap-menubar">
            <span class="sap-menu">Outbound Delivery</span>
            <span class="sap-menu">Edit</span>
            <span class="sap-menu">Goto</span>
            <span class="sap-menu">Extras</span>
            <span class="sap-menu">Subsequent</span>
            <span class="sap-menu">System</span>
            <span class="sap-menu">Help</span>
          </div>

          <div class="sap-toolbar">
            <button class="sap-tbn" onclick="navigate('sap-va01')">←</button>
            <button class="sap-tbn">🏠</button>
            <button class="sap-tbn">✕</button>
            <div class="sap-sep"></div>
            <button class="sap-tbn">🖨</button>
            <button class="sap-tbn">🔍</button>
            <div class="sap-sep"></div>
            <button class="sap-tbn">◄</button>
            <button class="sap-tbn">►</button>
            <div style="flex:1;"></div>
            <select class="sap-trx-select" onchange="navigate(this.value);this.value='sap-vl01n'">
              <option value="sap-va01">VA01/VA03 – Sales Orders</option>
              <option value="sap-vl01n" selected>VL01N – Check Delivery</option>
              <option value="sap-vl02n">VL02N – PGI Dispatch</option>
            </select>
          </div>

          <div class="sap-cmdbar">
            <div class="sap-cmdf">
              <div class="sap-cmd-icon">🔍</div>
              <input class="sap-cmd-input" id="vl01n-doc-input" style="width:200px;" readonly>
            </div>
            <button class="sap-enter-btn">Enter</button>
            <div style="flex:1;"></div>
            <select class="sap-trx-select" onchange="populateSap(this.value)">
              <option value="s001">Delivery 800025510 · OXXO Reforma</option>
              <option value="s002">Delivery 800033342 · OXXO Insurgentes</option>
              <option value="s003">Delivery 800031108 · OXXO Santa María</option>
              <option value="s004">Delivery 800022890 · OXXO Lerma</option>
              <option value="s005">Delivery 800020055 · OXXO Lerma 2</option>
            </select>
          </div>

          <div class="sap-form">
            <div class="sap-fr">
              <div class="sap-fg">
                <div class="sap-fl">Outbound Delivery</div>
                <input class="sap-fi" id="vl01n-deliv-num" style="width:95px;" readonly>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">Ship-to Party</div>
                <div style="display:flex;">
                  <input class="sap-fi" id="vl01n-shipto-id" style="width:62px;" readonly>
                  <span class="sap-fn" id="vl01n-shipto-name" style="min-width:200px;"></span>
                </div>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">Shipping Point</div>
                <input class="sap-fi" value="CAF1" style="width:50px;" readonly>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">Planned GI Date</div>
                <input class="sap-fi" id="vl01n-gi-date" style="width:90px;" readonly>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">Sales Order Ref.</div>
                <input class="sap-fi" id="vl01n-so-ref" style="width:95px;color:var(--sap-blue);font-weight:700;cursor:pointer;" onclick="navigate('sap-va01')" readonly>
              </div>
            </div>
          </div>

          <div class="sap-tabbar">
            <div class="sap-tab active" onclick="switchSapTab('vl01n','pick',this)">Picking</div>
            <div class="sap-tab" onclick="switchSapTab('vl01n','load',this)">Loading</div>
            <div class="sap-tab" onclick="switchSapTab('vl01n','transport',this)">Transport</div>
            <div class="sap-tab" onclick="switchSapTab('vl01n','status',this)">Status Overview</div>
            <div class="sap-tab" onclick="switchSapTab('vl01n','gm',this)">Goods Movement Data</div>
          </div>

          <div class="sap-tc active" id="vl01n-tab-pick">
            <div style="flex:1;overflow:auto;background:white;">
              <table class="sap-tbl-t">
                <thead>
                  <tr>
                    <th style="width:75px;">Item</th>
                    <th style="width:110px;">Material</th>
                    <th>Description</th>
                    <th style="width:80px;text-align:right;">Deliv. Qty</th>
                    <th style="width:40px;">Un</th>
                    <th style="width:75px;text-align:right;">Pick Qty</th>
                    <th style="width:100px;">Storage Loc.</th>
                    <th style="width:100px;">Batch</th>
                    <th style="width:100px;">Pick Status</th>
                  </tr>
                </thead>
                <tbody id="vl01n-tbody"></tbody>
              </table>
            </div>
          </div>

          <div class="sap-tc" id="vl01n-tab-load">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-form" style="border-bottom:none;"><div style="font-family:Arial;font-size:12px;color:#555;padding:6px 0;">No shipment assigned. Please use T-Code VT01N to create a shipment.</div></div>
            </div>
          </div>

          <div class="sap-tc" id="vl01n-tab-transport">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-form" style="border-bottom:none;">
                <div class="sap-fr">
                  <div class="sap-fg"><div class="sap-fl">Shipping Point</div><input class="sap-fi" value="CAF1" style="width:55px;" readonly></div>
                  <div class="sap-fg"><div class="sap-fl">Route</div><input class="sap-fi" value="MX001 — CDMX Std." style="width:180px;" readonly></div>
                  <div class="sap-fg"><div class="sap-fl">Means of Transport</div><input class="sap-fi" value="T — Road" style="width:110px;" readonly></div>
                </div>
              </div>
            </div>
          </div>

          <div class="sap-tc" id="vl01n-tab-status">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-form" style="border-bottom:none;">
                <div class="sap-fr" style="gap:12px;">
                  <div class="sap-fg"><div class="sap-fl">Overall Status</div><input class="sap-fi" value="B — Partially processed" style="width:200px;color:var(--sap-amber);font-weight:700;" readonly></div>
                  <div class="sap-fg"><div class="sap-fl">Picking Status</div><input class="sap-fi" value="C — Completely picked" style="width:200px;color:var(--sap-green);font-weight:700;" readonly></div>
                  <div class="sap-fg"><div class="sap-fl">GI Status</div><input class="sap-fi" value="A — Not yet started" style="width:180px;color:var(--sap-amber);font-weight:700;" readonly></div>
                </div>
              </div>
            </div>
          </div>

          <div class="sap-tc" id="vl01n-tab-gm">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-form" style="border-bottom:none;"><div style="font-family:Arial;font-size:12px;color:#555;padding:6px 0;">Goods movement data will be available after posting the Goods Issue in VL02N.</div></div>
            </div>
          </div>

          <div class="sap-statusbar">
            <div class="sap-st-icon sap-st-ok">S</div>
            <span class="sap-st-txt" id="vl01n-status-text">Delivery — Status: Ready for PGI</span>
            <div style="flex:1;"></div>
            <span style="font-size:10.5px;font-family:Arial;color:#666;">Client: CAF | User: JPALAO | T-Code: VL03N</span>
          </div>

        </div>
      </div>
    </div>

    <!-- ════ SAP VL02N – PGI DISPATCH ════ -->
    <div class="view" id="view-sap-vl02n">
      <div class="sap-wrap">
        <div class="sap-window">

          <div class="sap-titlebar">
            <div class="sap-titlebar-left">
              <div class="sap-win-icon" style="background:#FFF0E0;border:1px solid #F09030;">▶</div>
              <span class="sap-win-title">Change Outbound Delivery: Overview</span>
            </div>
            <div class="sap-wbtns"><div class="sap-wb">─</div><div class="sap-wb">□</div><div class="sap-wb">✕</div></div>
          </div>

          <div class="sap-menubar">
            <span class="sap-menu">Outbound Delivery</span>
            <span class="sap-menu">Edit</span>
            <span class="sap-menu">Goto</span>
            <span class="sap-menu">Subsequent</span>
            <span class="sap-menu">Post Goods Issue</span>
            <span class="sap-menu">System</span>
            <span class="sap-menu">Help</span>
          </div>

          <div class="sap-toolbar">
            <button class="sap-tbn" onclick="navigate('sap-vl01n')">←</button>
            <button class="sap-tbn">🏠</button>
            <button class="sap-tbn">✕</button>
            <div class="sap-sep"></div>
            <button class="sap-tbn" onclick="showToast('💾 Guardado')">💾</button>
            <button class="sap-tbn">🖨</button>
            <div class="sap-sep"></div>
            <button class="sap-tbn">◄</button>
            <button class="sap-tbn">►</button>
            <div class="sap-sep"></div>
            <button class="sap-gi-btn" onclick="postGI()">GI</button>
            <div style="flex:1;"></div>
            <select class="sap-trx-select" onchange="navigate(this.value);this.value='sap-vl02n'">
              <option value="sap-va01">VA01/VA03 – Sales Orders</option>
              <option value="sap-vl01n">VL01N – Check Delivery</option>
              <option value="sap-vl02n" selected>VL02N – PGI Dispatch</option>
            </select>
          </div>

          <div class="sap-cmdbar">
            <div class="sap-cmdf">
              <div class="sap-cmd-icon">🔍</div>
              <input class="sap-cmd-input" id="vl02n-doc-input" style="width:200px;" readonly>
            </div>
            <button class="sap-enter-btn">Enter</button>
            <button class="sap-pgi-btn" id="pgi-btn" onclick="postGI()">
              <svg width="11" height="11" viewBox="0 0 24 24" fill="currentColor"><polygon points="5 3 19 12 5 21 5 3"/></svg>
              Post Goods Issue
            </button>
            <div style="flex:1;"></div>
            <select class="sap-trx-select" onchange="populateSap(this.value)">
              <option value="s001">Delivery 800025510 · OXXO Reforma</option>
              <option value="s002">Delivery 800033342 · OXXO Insurgentes</option>
              <option value="s003">Delivery 800031108 · OXXO Santa María</option>
              <option value="s004">Delivery 800022890 · OXXO Lerma</option>
              <option value="s005">Delivery 800020055 · OXXO Lerma 2</option>
            </select>
          </div>

          <div class="sap-form">
            <div class="sap-fr">
              <div class="sap-fg">
                <div class="sap-fl">Outbound Delivery</div>
                <input class="sap-fi" id="vl02n-deliv-num" style="width:95px;" readonly>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">Ship-to Party</div>
                <div style="display:flex;">
                  <input class="sap-fi" id="vl02n-shipto-id" style="width:62px;" readonly>
                  <span class="sap-fn" id="vl02n-shipto-name" style="min-width:200px;"></span>
                </div>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">Shipping Point</div>
                <input class="sap-fi" value="CAF1" style="width:50px;" readonly>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">Planned GI</div>
                <input class="sap-fi" id="vl02n-gi-date" style="width:90px;" readonly>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">Total Weight</div>
                <input class="sap-fi" id="vl02n-weight" style="width:80px;" readonly>
              </div>
              <div class="sap-fg">
                <div class="sap-fl">GI Status</div>
                <span class="sap-fn" id="vl02n-gi-st" style="color:var(--sap-amber);font-weight:700;min-width:120px;">A — Open</span>
              </div>
            </div>
          </div>

          <div class="sap-tabbar">
            <div class="sap-tab active" onclick="switchSapTab('vl02n','items',this)">Picking</div>
            <div class="sap-tab" onclick="switchSapTab('vl02n','load',this)">Loading</div>
            <div class="sap-tab" onclick="switchSapTab('vl02n','transport',this)">Transport</div>
            <div class="sap-tab" onclick="switchSapTab('vl02n','status',this)">Status Overview</div>
            <div class="sap-tab" onclick="switchSapTab('vl02n','gm',this)">Goods Movement Data</div>
          </div>

          <div class="sap-tc active" id="vl02n-tab-items">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-info-bar">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="var(--sap-amber)" stroke-width="2"><circle cx="12" cy="12" r="10"/><line x1="12" y1="8" x2="12" y2="12"/><line x1="12" y1="16" x2="12.01" y2="16"/></svg>
                <span class="sap-info-txt">Post Goods Issue not yet executed. Click 「Post Goods Issue」 to execute movement type 601 (BAPI_GOODSMVT_CREATE).</span>
              </div>
              <table class="sap-tbl-t">
                <thead>
                  <tr>
                    <th style="width:75px;">Item</th>
                    <th style="width:110px;">Material</th>
                    <th>Description</th>
                    <th style="width:80px;text-align:right;">Deliv. Qty</th>
                    <th style="width:40px;">Un</th>
                    <th style="width:100px;">Storage Loc.</th>
                    <th style="width:100px;">Batch</th>
                    <th style="width:100px;">GI Status</th>
                  </tr>
                </thead>
                <tbody id="vl02n-tbody"></tbody>
              </table>
            </div>
          </div>

          <div class="sap-tc" id="vl02n-tab-load">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-form" style="border-bottom:none;"><div style="font-family:Arial;font-size:12px;color:#555;padding:6px 0;">No loading assigned. Please create a shipment first.</div></div>
            </div>
          </div>

          <div class="sap-tc" id="vl02n-tab-transport">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-form" style="border-bottom:none;">
                <div class="sap-fr">
                  <div class="sap-fg"><div class="sap-fl">Shipping Point</div><input class="sap-fi" value="CAF1" style="width:55px;" readonly></div>
                  <div class="sap-fg"><div class="sap-fl">Route</div><input class="sap-fi" value="MX001 — CDMX Std." style="width:180px;" readonly></div>
                </div>
              </div>
            </div>
          </div>

          <div class="sap-tc" id="vl02n-tab-status">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-form" style="border-bottom:none;">
                <div class="sap-fr" style="gap:12px;">
                  <div class="sap-fg"><div class="sap-fl">Overall Picking Status</div><input class="sap-fi" value="C — Completely picked" style="width:200px;color:var(--sap-green);font-weight:700;" readonly></div>
                  <div class="sap-fg"><div class="sap-fl">GI Status</div><span class="sap-fn" id="vl02n-gi-st2" style="color:var(--sap-amber);font-weight:700;min-width:180px;">A — Not yet started</span></div>
                </div>
              </div>
            </div>
          </div>

          <div class="sap-tc" id="vl02n-tab-gm">
            <div style="flex:1;overflow:auto;background:white;">
              <div class="sap-section">Goods Movements — Movement Type 601</div>
              <table class="sap-tbl-t">
                <thead>
                  <tr>
                    <th style="width:110px;">Material</th>
                    <th>Description</th>
                    <th style="width:70px;text-align:right;">Qty</th>
                    <th style="width:40px;">Un</th>
                    <th style="width:55px;">Mvt</th>
                    <th style="width:80px;">Acct Assgmt</th>
                    <th style="width:90px;text-align:right;">Amount</th>
                    <th style="width:110px;">Mat. Document</th>
                  </tr>
                </thead>
                <tbody id="vl02n-gm-tbody"><tr><td colspan="8" style="color:#999;text-align:center;padding:20px;font-family:Arial;font-size:12px;">GI not yet posted.</td></tr></tbody>
              </table>
            </div>
          </div>

          <div class="sap-statusbar">
            <div class="sap-st-icon" id="vl02n-st-icon" style="background:var(--sap-amber);">!</div>
            <span class="sap-st-txt" id="vl02n-status-text">Status: Open — Ready for PGI</span>
            <div style="flex:1;"></div>
            <span style="font-size:10.5px;font-family:Arial;color:#666;">Client: CAF | User: JPALAO | T-Code: VL02N</span>
          </div>

        </div>
      </div>
    </div>

  </div><!-- /content -->
</div><!-- /main -->

<!-- REPOSITORIO VIEW (inside content, already rendered by navigate) -->

<!-- PDF VIEWER FULL-SCREEN MODAL -->
<div class="pdf-modal-overlay" id="pdf-viewer-overlay">
  <div class="pdf-viewer-toolbar">
    <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#F87171" stroke-width="2" style="flex-shrink:0;"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14,2 14,8 20,8"/></svg>
    <span class="pdf-viewer-title" id="pdf-viewer-title">Orden de Compra OXXO</span>
    <div style="display:flex;align-items:center;gap:6px;background:rgba(255,255,255,.08);padding:4px 12px;border-radius:20px;border:1px solid rgba(255,255,255,.15);">
      <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="#4ADE80" stroke-width="2"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22,4 12,14.01 9,11.01"/></svg>
      <span style="font-size:11px;font-weight:600;color:#4ADE80;">Documento verificado</span>
    </div>
    <div style="display:flex;gap:4px;background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.1);border-radius:8px;padding:4px;">
      <button class="pdf-tb-btn" style="border:none;padding:5px 10px;" onclick="zoomPDF(-10)">−</button>
      <span id="pdf-zoom-level" style="color:rgba(255,255,255,.6);font-size:12px;min-width:40px;text-align:center;line-height:28px;">100%</span>
      <button class="pdf-tb-btn" style="border:none;padding:5px 10px;" onclick="zoomPDF(10)">+</button>
    </div>
    <button class="pdf-tb-btn" onclick="showToast('⬇️ Descargando PDF…')">
      <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
      Descargar
    </button>
    <button class="pdf-tb-btn pdf-tb-btn-orange" id="pdf-process-btn">
      <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="5 3 19 12 5 21 5 3"/></svg>
      Procesar en SAP
    </button>
    <button class="pdf-tb-btn" onclick="closePDFViewer()" style="margin-left:4px;">
      <svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
      Cerrar
    </button>
  </div>
  <div class="pdf-viewer-body" id="pdf-viewer-body"></div>
</div>

<!-- MODALS -->
<div class="modal-overlay" id="modal-detail"><div class="modal det-modal" style="padding:0;overflow:hidden;"><div class="modal-header" style="padding:18px 24px;"><div><div class="modal-title" id="detail-modal-title" style="font-size:17px;">📋 Detalle</div><div class="modal-sub" id="detail-modal-sub" style="margin-top:2px;"></div></div><button class="modal-close" onclick="closeModal('modal-detail')">✕</button></div><div class="modal-body" id="detail-modal-body" style="padding:0;max-height:72vh;overflow-y:auto;"></div><div class="modal-footer" style="padding:14px 20px;"><button class="btn btn-ghost" onclick="closeModal('modal-detail')">Cerrar</button><button class="btn btn-orange" style="font-size:13px;padding:8px 20px;" onclick="processFromDetail()">✓ Procesar Pedido</button></div></div></div>
<div class="modal-overlay" id="modal-error"><div class="modal"><div class="modal-header"><div><div class="modal-title" id="error-modal-title">⚠️ Validación</div><div class="modal-sub">Diagnóstico Agente IA</div></div><button class="modal-close" onclick="closeModal('modal-error')">✕</button></div><div class="modal-body" id="error-modal-body"></div><div class="modal-footer"><button class="btn btn-ghost" onclick="closeModal('modal-error')">Cancelar</button><button class="btn btn-orange" onclick="applyFix()">⚡ Aplicar Corrección</button></div></div></div>
<div class="modal-overlay" id="modal-fix"><div class="modal"><div class="modal-header"><div><div class="modal-title">🛠 Fix Anomaly</div><div class="modal-sub" id="fix-modal-sub">Agente IA</div></div><button class="modal-close" onclick="closeModal('modal-fix')">✕</button></div><div class="modal-body" id="fix-modal-body"></div><div class="modal-footer"><button class="btn btn-ghost" onclick="closeModal('modal-fix')">Cancelar</button><button class="btn btn-orange" onclick="confirmFix()">✅ Aplicar y Procesar</button></div></div></div>
<div class="modal-overlay" id="modal-logs"><div class="modal"><div class="modal-header"><div><div class="modal-title" id="logs-modal-title">Logs del Agente</div><div class="modal-sub">Historial de ejecución en tiempo real</div></div><button class="modal-close" onclick="closeModal('modal-logs')">✕</button></div><div class="modal-body" id="logs-modal-body"></div><div class="modal-footer"><button class="btn btn-ghost" onclick="closeModal('modal-logs')">Cerrar</button></div></div></div>
<div class="modal-overlay" id="modal-po"><div class="modal po-modal" style="max-width:860px;padding:0;border-radius:16px;overflow:hidden;"><div id="po-modal-body"></div><div class="modal-footer" style="border-radius:0;"><button class="btn btn-ghost" onclick="closeModal('modal-po')">Cerrar</button><button class="btn btn-dark" onclick="showToast('⬇️ Descargando PO como PDF…');closeModal('modal-po')"><svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>Descargar PO</button><button class="btn btn-orange" id="po-process-btn"><svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="5 3 19 12 5 21 5 3"/></svg>Procesar en SAP</button></div></div></div>
<div id="toast-container" class="hidden" style="position:fixed;bottom:24px;right:24px;z-index:9999;background:#111827;color:white;padding:12px 18px;border-radius:12px;font-size:13px;font-weight:500;box-shadow:0 8px 32px rgba(0,0,0,.3);display:flex;align-items:center;gap:10px;max-width:380px;transition:opacity .3s,transform .3s;transform:translateY(0);">
  <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="#4ADE80" stroke-width="2.5"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22,4 12,14.01 9,11.01"/></svg>
  <span id="toast-text">Acción completada</span>
</div>

<script>
// ════════════════════════════════════════════
//  DATA
// ════════════════════════════════════════════
const orders={
  s001:{sapNum:'100025255',uuid:'cd86b017',fromName:'OXXO de Paseo de la Reforma',soldToId:'100001',soldToName:'OXXO de Paseo de la Reforma',poNumber:'EXT-1234',orderDate:'23.04.2026',delivDate:'30.04.2026',netVal:'4,275.00',delivNum:'800025510',giDate:'2026-04-30',weight:'18.50 KG',
    items:[{pos:'10',sku:'PKG-602',desc:'Tapa Vaso 16oz (Caja 1000 pzs)',qty:1,unit:'CJ',price:'4,275.00',plant:'CAF1',delivDate:'30.04.2026',status:'Open'}],
    delivItems:[{pos:'000010',sku:'PKG-602',desc:'Tapa Vaso 16oz (Caja 1000 pzs)',qty:1,unit:'CJ',pickQty:1,sloc:'0001',batch:'L20260423'}]},
  s002:{sapNum:'100057527',uuid:'8ca64acb',fromName:'OXXO de Insurgentes Sur',soldToId:'100002',soldToName:'OXXO de Insurgentes Sur',poNumber:'OC-INS-20260423',orderDate:'23.04.2026',delivDate:'28.04.2026',netVal:'340.00',delivNum:'800033342',giDate:'2026-04-28',weight:'22.00 KG',
    items:[{pos:'10',sku:'LEC-001-1L',desc:'Leche Entera Ultra Pasteurizada 1L',qty:20,unit:'L',price:'340.00',plant:'CAF1',delivDate:'28.04.2026',status:'Completed'}],
    delivItems:[{pos:'000010',sku:'LEC-001-1L',desc:'Leche Entera UHT 1L',qty:20,unit:'L',pickQty:20,sloc:'0001',batch:'L20260420'},{pos:'000020',sku:'PKG-601',desc:'Vaso Térmico 12oz',qty:7,unit:'CJ',pickQty:7,sloc:'0002',batch:'L20260418'}]},
  s003:{sapNum:'100034317',uuid:'a5db2326',fromName:'OXXO Santa María',soldToId:'100003',soldToName:'OXXO Santa María',poNumber:'PC-SMA-2026-015',orderDate:'22.04.2026',delivDate:'26.04.2026',netVal:'255.00',delivNum:'800031108',giDate:'2026-04-26',weight:'15.50 KG',
    items:[{pos:'10',sku:'LEC-001-1L',desc:'Leche Entera Ultra Pasteurizada 1L',qty:15,unit:'L',price:'255.00',plant:'CAF1',delivDate:'26.04.2026',status:'Completed'}],
    delivItems:[{pos:'000010',sku:'LEC-001-1L',desc:'Leche Entera UHT 1L',qty:15,unit:'L',pickQty:15,sloc:'0001',batch:'L20260419'}]},
  s004:{sapNum:'100017625',uuid:'045ec45b',fromName:'OXXO Lerma MID',soldToId:'100004',soldToName:'OXXO Lerma MID',poNumber:'LER-OC-042',orderDate:'22.04.2026',delivDate:'25.04.2026',netVal:'520.00',delivNum:'800022890',giDate:'2026-04-25',weight:'21.00 KG',
    items:[{pos:'10',sku:'LAL-001-946',desc:'Leche de Almendra Unsweetened 946ml',qty:20,unit:'L',price:'520.00',plant:'CAF1',delivDate:'25.04.2026',status:'Completed'}],
    delivItems:[{pos:'000010',sku:'LAL-001-946',desc:'Leche Almendra 946ml',qty:20,unit:'L',pickQty:20,sloc:'0001',batch:'L20260417'}]},
  s005:{sapNum:'100058448',uuid:'feba249d',fromName:'OXXO Lerma MID',soldToId:'100004',soldToName:'OXXO Lerma MID',poNumber:'LER-OC-041',orderDate:'21.04.2026',delivDate:'24.04.2026',netVal:'5,125.00',delivNum:'800020055',giDate:'2026-04-24',weight:'115.00 KG',
    items:[{pos:'10',sku:'CAF-001-1KG',desc:'Café en Grano Mezcla Especial 1KG',qty:15,unit:'KG',price:'4,275.00',plant:'CAF1',delivDate:'24.04.2026',status:'Completed'},{pos:'20',sku:'AZU-050-KG',desc:'Azúcar Estándar Costal 50KG',qty:2,unit:'SAC',price:'850.00',plant:'CAF1',delivDate:'24.04.2026',status:'Completed'}],
    delivItems:[{pos:'000010',sku:'CAF-001-1KG',desc:'Café Grano Mezcla Especial 1KG',qty:15,unit:'KG',pickQty:15,sloc:'0001',batch:'L20260415'},{pos:'000020',sku:'AZU-050-KG',desc:'Azúcar Estándar 50KG',qty:2,unit:'SAC',pickQty:2,sloc:'0004',batch:'L20260412'}]}
};


// ════════════════════════════════════════════════════════════════════
//  CATÁLOGOS — 30 TIENDAS OXXO + 15 PRODUCTOS CAFFENIO
// ════════════════════════════════════════════════════════════════════
const OXXO_STORES=[
  // CDMX — 20 tiendas
  {id:'CDMX-01',name:'OXXO Paseo de la Reforma',city:'CDMX',zone:'Centro',addr:'Paseo de la Reforma 222, Juárez'},
  {id:'CDMX-02',name:'OXXO Insurgentes Sur',city:'CDMX',zone:'Sur',addr:'Insurgentes Sur 1602, Crédito Constructor'},
  {id:'CDMX-03',name:'OXXO Santa María la Ribera',city:'CDMX',zone:'Norte',addr:'Salvador Díaz Mirón 33, Sta. María la Ribera'},
  {id:'CDMX-04',name:'OXXO Polanco Norte',city:'CDMX',zone:'Centro',addr:'Masaryk 289, Polanco'},
  {id:'CDMX-05',name:'OXXO Constituyentes',city:'CDMX',zone:'Poniente',addr:'Av. Constituyentes 850, Lomas Altas'},
  {id:'CDMX-06',name:'OXXO Satélite Centro',city:'EDOMEX',zone:'Norte',addr:'Circuito Médicos 3, Cd. Satélite, Naucalpan'},
  {id:'CDMX-07',name:'OXXO Naucalpan Industrial',city:'EDOMEX',zone:'Norte',addr:'Av. Lázaro Cárdenas 103, Naucalpan'},
  {id:'CDMX-08',name:'OXXO Tlalnepantla',city:'EDOMEX',zone:'Norte',addr:'Blvd. Manuel Ávila Camacho 90, Tlalnepantla'},
  {id:'CDMX-09',name:'OXXO Lerma MID',city:'EDOMEX',zone:'Poniente',addr:'Blvd. Miguel Hidalgo 22, Lerma'},
  {id:'CDMX-10',name:'OXXO Ecatepec Centro',city:'EDOMEX',zone:'Oriente',addr:'Av. Central 55, Ecatepec'},
  {id:'CDMX-11',name:'OXXO Ciudad Universitaria',city:'CDMX',zone:'Sur',addr:'Copilco 150, Coyoacán'},
  {id:'CDMX-12',name:'OXXO Pedregal',city:'CDMX',zone:'Sur',addr:'Periférico Sur 3720, Pedregal de San Ángel'},
  {id:'CDMX-13',name:'OXXO Xochimilco',city:'CDMX',zone:'Sur',addr:'Pino 35, Barrio San Pedro Xochimilco'},
  {id:'CDMX-14',name:'OXXO Iztapalapa Sur',city:'CDMX',zone:'Oriente',addr:'Ermita Iztapalapa 1250, Iztapalapa'},
  {id:'CDMX-15',name:'OXXO Venustiano Carranza',city:'CDMX',zone:'Oriente',addr:'Fray Servando Teresa de Mier 422, V.Carranza'},
  {id:'CDMX-16',name:'OXXO Doctores',city:'CDMX',zone:'Centro',addr:'Dr. Erazo 90, Doctores'},
  {id:'CDMX-17',name:'OXXO La Condesa',city:'CDMX',zone:'Centro',addr:'Tamaulipas 95, Hipódromo Condesa'},
  {id:'CDMX-18',name:'OXXO Roma Norte',city:'CDMX',zone:'Centro',addr:'Álvaro Obregón 171, Roma Norte'},
  {id:'CDMX-19',name:'OXXO Nápoles',city:'CDMX',zone:'Sur',addr:'Xola 612, Nápoles'},
  {id:'CDMX-20',name:'OXXO Serv. Adm. Central',city:'CDMX',zone:'Centro',addr:'Ejército Nacional 843-B, Polanco'},
  // Monterrey — 6 tiendas
  {id:'MTY-01',name:'OXXO Garza García',city:'Monterrey',zone:'Norte',addr:'Av. Vasconcelos 101 Ote., Garza García'},
  {id:'MTY-02',name:'OXXO Valle Oriente',city:'Monterrey',zone:'Sur',addr:'Av. Lázaro Cárdenas 1000, Valle Oriente'},
  {id:'MTY-03',name:'OXXO Mitras Centro',city:'Monterrey',zone:'Centro',addr:'Av. Félix U. Gómez 315, Mitras Centro'},
  {id:'MTY-04',name:'OXXO San Nicolás',city:'Monterrey',zone:'Norte',addr:'Universidad 701, San Nicolás de los Garza'},
  {id:'MTY-05',name:'OXXO Guadalupe MTY',city:'Monterrey',zone:'Oriente',addr:'Av. Pablo González 820, Guadalupe'},
  {id:'MTY-06',name:'OXXO Apodaca MTY',city:'Monterrey',zone:'Norte',addr:'Blvd. Díaz Ordaz 130, Apodaca'},
  // Guadalajara — 4 tiendas
  {id:'GDL-01',name:'OXXO Zapopan',city:'Guadalajara',zone:'Norte',addr:'Av. Patria 1501, Zapopan'},
  {id:'GDL-02',name:'OXXO Tlaquepaque',city:'Guadalajara',zone:'Sur',addr:'Independencia 130, San Pedro Tlaquepaque'},
  {id:'GDL-03',name:'OXXO Tonalá',city:'Guadalajara',zone:'Oriente',addr:'Av. Tonaltecas 350, Tonalá'},
  {id:'GDL-04',name:'OXXO Tlajomulco',city:'Guadalajara',zone:'Sur',addr:'Av. López Mateos Sur 6700, Tlajomulco'}
];

const CAFFENIO_PRODUCTS=[
  {sku:'CAF-001-1KG', desc:'Café en Grano Mezcla Especial 1KG',     um:'KG',  price:285,  minQ:5,  maxQ:50},
  {sku:'CAF-MOL-500G',desc:'Café Molido Espresso Blend 500G',        um:'PZS', price:142,  minQ:10, maxQ:120},
  {sku:'CAF-CAP-1KG', desc:'Café Cápsulas Compatibles 1KG',          um:'BOX', price:320,  minQ:5,  maxQ:30},
  {sku:'CAF-ESP-250G',desc:'Café Espresso Intenso 250G',              um:'PZS', price:95,   minQ:20, maxQ:200},
  {sku:'LEC-001-1L',  desc:'Leche Entera Ultra Pasteurizada 1L',      um:'L',   price:17,   minQ:24, maxQ:480},
  {sku:'LEC-DES-1L',  desc:'Leche Deslactosada UHT 1L',              um:'L',   price:19,   minQ:24, maxQ:240},
  {sku:'LAL-001-946', desc:'Leche de Almendra Unsweetened 946ml',     um:'PZS', price:26,   minQ:12, maxQ:96},
  {sku:'AZU-050-KG',  desc:'Azúcar Estándar Costal 50KG',            um:'COS', price:425,  minQ:1,  maxQ:10},
  {sku:'SAC-001-1KG', desc:'Sacarina Natural 1KG',                    um:'KG',  price:185,  minQ:2,  maxQ:20},
  {sku:'PKG-602',     desc:'Tapa Vaso 16oz (Caja 1000 pzs)',          um:'CJ',  price:4275, minQ:1,  maxQ:5},
  {sku:'PKG-601',     desc:'Vaso Térmico 12oz (Caja 100 pzs)',        um:'CJ',  price:480,  minQ:1,  maxQ:10},
  {sku:'PKG-603',     desc:'Tapa Vaso 12oz (Caja 1000 pzs)',          um:'CJ',  price:3850, minQ:1,  maxQ:5},
  {sku:'VAS-012-50PK',desc:'Vaso Térmico 16oz (Paquete 50 pzs)',      um:'PKT', price:240,  minQ:2,  maxQ:20},
  {sku:'CRE-001-500', desc:'Crema Media Crema 500ml',                 um:'L',   price:22,   minQ:24, maxQ:200},
  {sku:'SER-NAP-500', desc:'Servilletas Kraft (Paquete 500)',          um:'PKT', price:85,   minQ:5,  maxQ:50}
];

// ════════════════════════════════════════════════════════════════════
//  10 DÍAS DE OPERACIÓN — 21 al 30 de Abril 2026
//  Base mensual: ~4,100 pedidos OXXO → ~1,400 en 10 días
// ════════════════════════════════════════════════════════════════════
const TEN_DAYS=[
  {d:'21/04/2026',label:'Lun 21 Abr',short:'L21',n:178,isWE:false,col:'#22C55E'},
  {d:'22/04/2026',label:'Mar 22 Abr',short:'M22',n:162,isWE:false,col:'#22C55E'},
  {d:'23/04/2026',label:'Mié 23 Abr',short:'X23',n:158,isWE:false,col:'#22C55E'},
  {d:'24/04/2026',label:'Jue 24 Abr',short:'J24',n:189,isWE:false,col:'#F59E0B'},
  {d:'25/04/2026',label:'Vie 25 Abr',short:'V25',n:143,isWE:false,col:'#22C55E'},
  {d:'26/04/2026',label:'Sáb 26 Abr',short:'S26',n:48, isWE:true, col:'#6B7280'},
  {d:'27/04/2026',label:'Dom 27 Abr',short:'D27',n:18, isWE:true, col:'#374151'},
  {d:'28/04/2026',label:'Lun 28 Abr',short:'L28',n:185,isWE:false,col:'#F97316'},
  {d:'29/04/2026',label:'Mar 29 Abr',short:'M29',n:167,isWE:false,col:'#22C55E'},
  {d:'30/04/2026',label:'Mié 30 Abr',short:'X30',n:152,isWE:false,col:'#22C55E'}
];
// Total: 1,400 pedidos en 10 días

const ERR_CODES=['MAT-SKU-404','CUST-MAP-001','PRC-COND-002','STO-CHK-003'];
const ERR_TITLES={'MAT-SKU-404':'Material Master Not Found','CUST-MAP-001':'Customer Mapping Anomaly','PRC-COND-002':'Price Condition Error','STO-CHK-003':'Stock Insufficient'};
const ERR_MSGS={
  'MAT-SKU-404':'El SKU solicitado no existe en el maestro de materiales (MARA). Posible error tipográfico o material descontinuado.',
  'CUST-MAP-001':'El remitente del correo no está en la whitelist de clientes habilitados en KNA1.',
  'PRC-COND-002':'No se encontró condición de precio vigente (KONP) para la combinación cliente/material solicitada.',
  'STO-CHK-003':'Stock disponible insuficiente para cubrir la cantidad solicitada. Verificar MMBE en almacén CAF1.'
};

// ════════════════════════════════════════════════════════════════════
//  DATASET — 1,400 órdenes determinísticas (21-30 Abr 2026)
//  Generado con PRNG semilla fija → reproducible sin Math.random()
// ════════════════════════════════════════════════════════════════════
(function buildDataset(){
  let seed = 0x4CAF50;
  const rand = () => { seed = (seed * 1664525 + 1013904223) & 0xFFFFFFFF; return (seed >>> 0) / 4294967296; };
  const pick = arr => arr[Math.floor(rand() * arr.length)];
  const rng  = (a, b) => a + Math.floor(rand() * (b - a + 1));

  const CITY_SHORT = { 'CDMX':'CDMX','EDOMEX':'EDOMEX','Monterrey':'MTY','Guadalajara':'GDL' };

  const all = [], backlog = [], errors = [];
  let sapN = 100025256;

  TEN_DAYS.forEach(day => {
    const isWE = day.isWE;
    for (let i = 0; i < day.n; i++) {
      const store   = pick(OXXO_STORES);
      const product = pick(CAFFENIO_PRODUCTS);
      const qty     = rng(product.minQ, Math.min(product.minQ * 3, product.maxQ));
      const totalMXN = Math.round(product.price * qty * (1 + rand() * 0.12) * 100) / 100;

      const r = rand();
      const status = isWE
        ? (r < 0.50 ? 'backlog' : r < 0.75 ? 'error' : 'success')
        : (r < 0.83 ? 'success' : r < 0.92 ? 'backlog' : 'error');

      const city      = store.city;
      const areaShort = CITY_SHORT[city] || city.substring(0,4).toUpperCase();
      // Short store code for OC number (e.g. OXXO Paseo → PAS)
      const storeCode = store.name.replace('OXXO ','').substring(0,3).toUpperCase().replace(/\s/g,'');
      // Multi-item order: 1-3 products
      const itemCount = rng(1, 3);
      const orderItems = [];
      let orderTotal = 0;
      const usedSkus = new Set();
      for(let k=0; k<itemCount; k++){
        let p2 = pick(CAFFENIO_PRODUCTS);
        let tries = 0;
        while(usedSkus.has(p2.sku) && tries++ < 8) p2 = pick(CAFFENIO_PRODUCTS);
        usedSkus.add(p2.sku);
        const q2 = rng(p2.minQ, Math.min(p2.minQ * 2, p2.maxQ));
        const lineTotal = Math.round(p2.price * q2 * (1 + rand() * 0.08) * 100) / 100;
        orderItems.push({ sku: p2.sku, desc: p2.desc, qty: q2, price: p2.price, total: lineTotal });
        orderTotal += lineTotal;
      }
      orderTotal = Math.round(orderTotal * 100) / 100;
      // Sub-status for backlog: 'pending' (70%) or 'warn' (30%)
      const subStatus = status === 'backlog'
        ? (rand() < 0.30 ? 'warn' : 'pending')
        : null;
      // Received time (business hours)
      const recvHour = rng(7, 17);
      const recvMin  = rng(0, 59);
      const recvTime = String(recvHour).padStart(2,'0') + ':' + String(recvMin).padStart(2,'0');
      const o = {
        sapNum        : String(sapN++),
        fromName      : store.name,
        storeCity     : city,
        zone          : store.zone,
        areaShort     : areaShort,
        poNumber      : 'OC-OXXO-' + storeCode + '-2026-' + String(sapN-100025256).padStart(4,'0'),
        date          : day.d,
        recvTime      : recvTime,
        sku           : orderItems[0].sku,
        status        : status,
        subStatus     : subStatus,
        soNumber      : status === 'success' ? 'SO-' + String(sapN + 900000) : null,
        totalMXN      : orderTotal,
        processingTime: status === 'success' ? Math.round((0.8 + rand() * 6.2) * 10) / 10 : 0,
        errorCode     : status === 'error' ? pick(ERR_CODES) : null,
        items         : orderItems
      };
      all.push(o);
      if (status === 'backlog') backlog.push(o);
      if (status === 'error')   errors.push(o);
    }
  });

  window.DATASET    = { all, success: all.filter(o=>o.status==='success'), errors, backlog };
  window.backlogData = backlog;
  window.errorsData  = errors;

  window.DAY_STATS = TEN_DAYS.map(day => {
    const dayOrds = all.filter(o => o.date === day.d);
    return {
      date   : day.d,
      label  : day.label,
      short  : day.short,
      dow    : day.label,
      vol    : dayOrds.length,
      total  : dayOrds.length,
      success: dayOrds.filter(o => o.status === 'success').length,
      backlog: dayOrds.filter(o => o.status === 'backlog').length,
      errors : dayOrds.filter(o => o.status === 'error').length
    };
  });
})();


function _rng(a,b){return Math.floor(Math.random()*(b-a+1))+a;}

function mkEmailBody(area){
  return 'De: Rommel Gil Vera <rommel.gil.vera@emeal.nttdata.com>\nPara: pedidos@caffenio.com\nCC: operaciones.proveedores@oxxo.com.mx\nAsunto: RV: Pedidos OXXO marca propia - '+area+'\nFecha: Miércoles, 30 de abril de 2026 — 09:14 hrs\n\nBuen día!\n\nEl motivo de mi correo es para enviarles el pedido correspondiente a esta semana, por consiguiente les pido confirmación de los siguientes puntos:\n\n  - Confirmación de Recibido\n  - Agendar dentro de las siguientes 48 hrs la cita de entrega,\n    favor de confirmar dicha fecha.\n\nSin más por el momento quedo a sus órdenes para cualquier duda o aclaración, que tengan buen día.\n\nGracias...\n\n⚠ Importante: Para entrega de proveedor es necesario el uso de\n  zapato con casquillo de acero (zapato cerrado).\n\nQuedo al pendiente,\n\nRommel Gil Vera | NTT Data\nOn behalf of OXXO Servicios Administrativos\nOXXO | Uso Interno — Información confidencial';
}



// ════════════════════════════════════════════
//  ORACLE RETAIL PO DATA (FEMSA Comercio)
// ════════════════════════════════════════════



const ORACLE_PO_DATA={
  'po-agu':{
    id:'po-agu',orderNo:'76933176',site:'SERVICIOS ADMINISTRATIVOS 15AGU 216510',
    file:'76933176_FA216510_04142026_SERVICIOS_ADMINISTRATIVOS_15AGU-.pdf',
    vendor:'101041',contact:'PRECIADO NORA',phone:'6622890740',fax:'66-22890740',
    notAfter:'22-Apr-2026',notBefore:'14-Apr-2026',terms:'30 dias',discount:'0.00',
    total:'143,544.11',location:'Aguascalientes',
    shipTo:'Aguascalientes AGS 20230',addr:'Blvd. Aguascalientes Sur 3603\nFracc. Pulgas Pandas Sur',
    items:[{qty:16,pack:12,uop:'CS',desc:'Cafe Molido Andatti 250gr',item:'7501954906644',dept:623,cost:1221.60,ext:19545.60},
    {qty:19,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 50 g',item:'7501954908600',dept:623,cost:448.80,ext:8527.20},
    {qty:22,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 100 g',item:'7501954908617',dept:623,cost:785.40,ext:17278.80},
    {qty:40,pack:60,uop:'CS',desc:'Cafe soluble andatti Sachet 35 g',item:'7501954909409',dept:623,cost:522.00,ext:20880.00},
    {qty:5,pack:12,uop:'CS',desc:'Cafe soluble descafeinado andatti 100g',item:'7501954910016',dept:623,cost:943.68,ext:4718.40},
    {qty:8,pack:80,uop:'CS',desc:'Capuchino clasico andatti 25gr',item:'7501954910214',dept:623,cost:580.19,ext:4641.54},
    {qty:3,pack:80,uop:'CS',desc:'Chocolate clasico andatti 25g',item:'7501954910238',dept:1188,cost:580.80,ext:1742.40},
    {qty:11,pack:60,uop:'CS',desc:'Cafe soluble descaf andatti Sachet 35g',item:'7501954910344',dept:623,cost:542.40,ext:5966.40},
    {qty:6,pack:12,uop:'CS',desc:'Cafe molido descafeinado andatti 250gr',item:'7502271151212',dept:623,cost:1368.24,ext:8209.44},
    {qty:8,pack:12,uop:'CS',desc:'Cafe andatti soluble descafeinado 50g',item:'7502271151601',dept:623,cost:524.04,ext:4192.32},
    {qty:3,pack:80,uop:'CS',desc:'Capuchino descafeinado andatti 25gr',item:'7502271152448',dept:623,cost:580.19,ext:1740.58},
    {qty:9,pack:80,uop:'CS',desc:'Sachet andatti capuchino vainilla 25gr',item:'7502271152455',dept:623,cost:580.19,ext:5221.73},
    {qty:14,pack:9,uop:'CS',desc:'Cafe Soluble Andatti 275g',item:'7502271155920',dept:623,cost:1215.72,ext:17020.08},
    {qty:8,pack:80,uop:'CS',desc:'Sachet andatti capuchino Moka 25gr',item:'7502271159577',dept:623,cost:580.19,ext:4641.54},
    {qty:2,pack:9,uop:'CS',desc:'Cafe Soluble Andatti Descafeinado 275g',item:'7502294221763',dept:623,cost:1467.63,ext:2935.26},
    {qty:4,pack:80,uop:'CS',desc:'Sachet andatti capuchino Canela 25g',item:'7502294223750',dept:623,cost:580.19,ext:2320.77},
    {qty:5,pack:80,uop:'CS',desc:'Sachet andatti capuchino Caramelo 25g',item:'7502294223767',dept:623,cost:580.19,ext:2900.96},
    {qty:3,pack:80,uop:'CS',desc:'CAPUCHINO FRIO REGULAR SACHET 25 G.',item:'7502294225778',dept:623,cost:642.04,ext:1926.13},
    {qty:3,pack:80,uop:'CS',desc:'CAPUCHINO FRIO VAINILLA SACHET 25 G.',item:'7502294225785',dept:623,cost:642.04,ext:1926.13},
    {qty:2,pack:80,uop:'CS',desc:'CAPUCHINO FRIO MOKA SACHET 25 G.',item:'7502294225792',dept:623,cost:642.04,ext:1284.08},
    {qty:1,pack:80,uop:'CS',desc:'CAPUCHINO AVELLANAS ANDATTI 25G',item:'7502294228007',dept:623,cost:642.04,ext:642.04}]
  },
  'po-tqv':{
    id:'po-tqv',orderNo:'76933072',site:'SERVICIOS ADMINISTRATIVOS 15TQV 30481',
    file:'76933072_FA30481_04142026_SERVICIOS_ADMINISTRATIVOS_15TQV.pdf',
    vendor:'101041',contact:'PRECIADO NORA',phone:'6622890740',fax:'66-22890740',
    notAfter:'20-Apr-2026',notBefore:'14-Apr-2026',terms:'30 dias',discount:'0.00',
    total:'348,257.85',location:'Querétaro',
    shipTo:'Queretaro QRO 76000',addr:'Av. Industria Minera 501\nFragg. Ampl. Industrial Fase 1',
    items:[{qty:38,pack:12,uop:'CS',desc:'Cafe Molido Andatti 250gr',item:'7501954906644',dept:623,cost:1221.60,ext:46420.80},
    {qty:46,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 50 g',item:'7501954908600',dept:623,cost:448.80,ext:20644.80},
    {qty:46,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 100 g',item:'7501954908617',dept:623,cost:785.40,ext:36128.40},
    {qty:65,pack:60,uop:'CS',desc:'Cafe soluble andatti Sachet 35 g',item:'7501954909409',dept:623,cost:522.00,ext:33930.00},
    {qty:7,pack:12,uop:'CS',desc:'Cafe soluble descafeinado andatti 100g',item:'7501954910016',dept:623,cost:943.68,ext:6605.76},
    {qty:13,pack:80,uop:'CS',desc:'Capuchino clasico andatti 25gr',item:'7501954910214',dept:623,cost:580.19,ext:7542.50},
    {qty:5,pack:80,uop:'CS',desc:'Chocolate clasico andatti 25g',item:'7501954910238',dept:1188,cost:580.80,ext:2904.00},
    {qty:23,pack:60,uop:'CS',desc:'Cafe soluble descaf andatti Sachet 35g',item:'7501954910344',dept:623,cost:542.40,ext:12475.20},
    {qty:11,pack:12,uop:'CS',desc:'Cafe molido descafeinado andatti 250gr',item:'7502271151212',dept:623,cost:1368.24,ext:15050.64},
    {qty:17,pack:12,uop:'CS',desc:'Cafe andatti soluble descafeinado 50g',item:'7502271151601',dept:623,cost:524.04,ext:8908.68},
    {qty:6,pack:80,uop:'CS',desc:'Capuchino descafeinado andatti 25gr',item:'7502271152448',dept:623,cost:580.19,ext:3481.15},
    {qty:21,pack:80,uop:'CS',desc:'Sachet andatti capuchino vainilla 25gr',item:'7502271152455',dept:623,cost:580.19,ext:12184.03},
    {qty:60,pack:9,uop:'CS',desc:'Cafe Soluble Andatti 275g',item:'7502271155920',dept:623,cost:1215.72,ext:72943.20},
    {qty:19,pack:80,uop:'CS',desc:'Sachet andatti capuchino Moka 25gr',item:'7502271159577',dept:623,cost:580.19,ext:11023.65},
    {qty:8,pack:9,uop:'CS',desc:'Cafe Soluble Andatti Descafeinado 275g',item:'7502294221763',dept:623,cost:1467.63,ext:11741.04},
    {qty:9,pack:80,uop:'CS',desc:'Sachet andatti capuchino Canela 25g',item:'7502294223750',dept:623,cost:580.19,ext:5221.73},
    {qty:11,pack:80,uop:'CS',desc:'Sachet andatti capuchino Caramelo 25g',item:'7502294223767',dept:623,cost:580.19,ext:6382.11},
    {qty:16,pack:80,uop:'CS',desc:'CAPUCHINO FRIO REGULAR SACHET 25 G.',item:'7502294225778',dept:623,cost:642.04,ext:10272.64},
    {qty:12,pack:80,uop:'CS',desc:'CAPUCHINO FRIO VAINILLA SACHET 25 G.',item:'7502294225785',dept:623,cost:642.04,ext:7704.48},
    {qty:18,pack:80,uop:'CS',desc:'CAPUCHINO FRIO MOKA SACHET 25 G.',item:'7502294225792',dept:623,cost:642.04,ext:11556.72},
    {qty:8,pack:80,uop:'CS',desc:'CAPUCHINO AVELLANAS ANDATTI 25G',item:'7502294228007',dept:623,cost:642.04,ext:5136.32}]
  },
  'po-vcz':{
    id:'po-vcz',orderNo:'76933173',site:'SERVICIOS ADMINISTRATIVOS 15VCZ 45858',
    file:'76933173_FA45858_04142026_SERVICIOS_ADMINISTRATIVOS_15VCZ.pdf',
    vendor:'101041',contact:'PRECIADO NORA',phone:'6622890740',fax:'66-22890740',
    notAfter:'21-Apr-2026',notBefore:'14-Apr-2026',terms:'30 dias',discount:'0.00',
    total:'300,534.58',location:'Veracruz',
    shipTo:'Veracruz VER 91700',addr:'Av. Universidad 1901\nBoca del Río',
    items:[{qty:30,pack:12,uop:'CS',desc:'Cafe Molido Andatti 250gr',item:'7501954906644',dept:623,cost:1221.60,ext:36648.00},
    {qty:35,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 50 g',item:'7501954908600',dept:623,cost:448.80,ext:15708.00},
    {qty:46,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 100 g',item:'7501954908617',dept:623,cost:785.40,ext:36128.40},
    {qty:112,pack:60,uop:'CS',desc:'Cafe soluble andatti Sachet 35 g',item:'7501954909409',dept:623,cost:522.00,ext:58464.00},
    {qty:15,pack:12,uop:'CS',desc:'Cafe soluble descafeinado andatti 100g',item:'7501954910016',dept:623,cost:943.68,ext:14155.20},
    {qty:10,pack:80,uop:'CS',desc:'Capuchino clasico andatti 25gr',item:'7501954910214',dept:623,cost:580.19,ext:5801.92},
    {qty:4,pack:80,uop:'CS',desc:'Chocolate clasico andatti 25g',item:'7501954910238',dept:1188,cost:580.80,ext:2323.20},
    {qty:30,pack:60,uop:'CS',desc:'Cafe soluble descaf andatti Sachet 35g',item:'7501954910344',dept:623,cost:542.40,ext:16272.00},
    {qty:8,pack:12,uop:'CS',desc:'Cafe molido descafeinado andatti 250gr',item:'7502271151212',dept:623,cost:1368.24,ext:10945.92},
    {qty:15,pack:12,uop:'CS',desc:'Cafe andatti soluble descafeinado 50g',item:'7502271151601',dept:623,cost:524.04,ext:7860.60},
    {qty:4,pack:80,uop:'CS',desc:'Capuchino descafeinado andatti 25gr',item:'7502271152448',dept:623,cost:580.19,ext:2320.77},
    {qty:14,pack:80,uop:'CS',desc:'Sachet andatti capuchino vainilla 25gr',item:'7502271152455',dept:623,cost:580.19,ext:8122.69},
    {qty:52,pack:9,uop:'CS',desc:'Cafe Soluble Andatti 275g',item:'7502271155920',dept:623,cost:1215.72,ext:63217.44},
    {qty:14,pack:80,uop:'CS',desc:'Sachet andatti capuchino Moka 25gr',item:'7502271159577',dept:623,cost:580.19,ext:8122.69},
    {qty:5,pack:9,uop:'CS',desc:'Cafe Soluble Andatti Descafeinado 275g',item:'7502294221763',dept:623,cost:1467.63,ext:7338.15},
    {qty:6,pack:80,uop:'CS',desc:'Sachet andatti capuchino Canela 25g',item:'7502294223750',dept:623,cost:580.19,ext:3481.15},
    {qty:9,pack:80,uop:'CS',desc:'Sachet andatti capuchino Caramelo 25g',item:'7502294223767',dept:623,cost:580.19,ext:5221.73},
    {qty:6,pack:80,uop:'CS',desc:'CAPUCHINO FRIO REGULAR SACHET 25 G.',item:'7502294225778',dept:623,cost:642.04,ext:3852.24},
    {qty:4,pack:80,uop:'CS',desc:'CAPUCHINO FRIO VAINILLA SACHET 25 G.',item:'7502294225785',dept:623,cost:642.04,ext:2568.16},
    {qty:5,pack:80,uop:'CS',desc:'CAPUCHINO FRIO MOKA SACHET 25 G.',item:'7502294225792',dept:623,cost:642.04,ext:3210.20},
    {qty:2,pack:80,uop:'CS',desc:'CAPUCHINO AVELLANAS ANDATTI 25G',item:'7502294228007',dept:623,cost:642.04,ext:1284.08}]
  },
  'po-obq':{
    id:'po-obq',orderNo:'76933065',site:'SERVICIOS ADMINISTRATIVOS 15OBQ 11309',
    file:'76933065_FA11309_04142026_SERVICIOS_ADMINISTRATIVOS_15OBQ.pdf',
    vendor:'101041',contact:'PRECIADO NORA',phone:'6622890740',fax:'66-22890740',
    notAfter:'21-Apr-2026',notBefore:'14-Apr-2026',terms:'30 dias',discount:'0.00',
    total:'533,410.72',location:'Obregón',
    shipTo:'Obregon SON 85050',addr:'Calzada Fco Villanueva Castelo\n#2054 Parque Industrial',
    items:[{qty:69,pack:12,uop:'CS',desc:'Cafe Molido Andatti 250gr',item:'7501954906644',dept:623,cost:1221.60,ext:84290.40},
    {qty:99,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 50 g',item:'7501954908600',dept:623,cost:448.80,ext:44431.20},
    {qty:95,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 100 g',item:'7501954908617',dept:623,cost:785.40,ext:74613.00},
    {qty:109,pack:60,uop:'CS',desc:'Cafe soluble andatti Sachet 35 g',item:'7501954909409',dept:623,cost:522.00,ext:56898.00},
    {qty:32,pack:12,uop:'CS',desc:'Cafe soluble descafeinado andatti 100g',item:'7501954910016',dept:623,cost:943.68,ext:30197.76},
    {qty:14,pack:80,uop:'CS',desc:'Capuchino clasico andatti 25gr',item:'7501954910214',dept:623,cost:580.19,ext:8122.69},
    {qty:8,pack:80,uop:'CS',desc:'Chocolate clasico andatti 25g',item:'7501954910238',dept:1188,cost:580.80,ext:4646.40},
    {qty:27,pack:60,uop:'CS',desc:'Cafe soluble descaf andatti Sachet 35g',item:'7501954910344',dept:623,cost:542.40,ext:14644.80},
    {qty:18,pack:12,uop:'CS',desc:'Cafe molido descafeinado andatti 250gr',item:'7502271151212',dept:623,cost:1368.24,ext:24628.32},
    {qty:36,pack:12,uop:'CS',desc:'Cafe andatti soluble descafeinado 50g',item:'7502271151601',dept:623,cost:524.04,ext:18865.44},
    {qty:5,pack:80,uop:'CS',desc:'Capuchino descafeinado andatti 25gr',item:'7502271152448',dept:623,cost:580.19,ext:2900.96},
    {qty:20,pack:80,uop:'CS',desc:'Sachet andatti capuchino vainilla 25gr',item:'7502271152455',dept:623,cost:580.19,ext:11603.84},
    {qty:99,pack:9,uop:'CS',desc:'Cafe Soluble Andatti 275g',item:'7502271155920',dept:623,cost:1215.72,ext:120356.28},
    {qty:18,pack:80,uop:'CS',desc:'Sachet andatti capuchino Moka 25gr',item:'7502271159577',dept:623,cost:580.19,ext:10443.46},
    {qty:6,pack:9,uop:'CS',desc:'Cafe Soluble Andatti Descafeinado 275g',item:'7502294221763',dept:623,cost:1467.63,ext:8805.78},
    {qty:6,pack:80,uop:'CS',desc:'Sachet andatti capuchino Canela 25g',item:'7502294223750',dept:623,cost:580.19,ext:3481.15},
    {qty:15,pack:80,uop:'CS',desc:'Sachet andatti capuchino Caramelo 25g',item:'7502294223767',dept:623,cost:580.19,ext:8702.88},
    {qty:2,pack:80,uop:'CS',desc:'CAPUCHINO FRIO REGULAR SACHET 25 G.',item:'7502294225778',dept:623,cost:642.04,ext:1284.08},
    {qty:1,pack:80,uop:'CS',desc:'CAPUCHINO FRIO VAINILLA SACHET 25 G.',item:'7502294225785',dept:623,cost:642.04,ext:642.04},
    {qty:1,pack:80,uop:'CS',desc:'CAPUCHINO FRIO MOKA SACHET 25 G.',item:'7502294225792',dept:623,cost:642.04,ext:642.04},
    {qty:5,pack:80,uop:'CS',desc:'CAPUCHINO AVELLANAS ANDATTI 25G',item:'7502294228007',dept:623,cost:642.04,ext:3210.20}]
  },
  'po-vhd':{
    id:'po-vhd',orderNo:'76933070',site:'SERVICIOS ADMINISTRATIVOS 15VHD- 20557',
    file:'76933070_FA20557_04142026_SERVICIOS_ADMINISTRATIVOS_15VHD-.pdf',
    vendor:'101041',contact:'PRECIADO NORA',phone:'6622890740',fax:'66-22890740',
    notAfter:'22-Apr-2026',notBefore:'14-Apr-2026',terms:'30 dias',discount:'0.00',
    total:'464,327.87',location:'Villahermosa',
    shipTo:'Cunduacan TAB 8669',addr:'Circuito Tabasco Pte MZA 5 L.1\nTabasco Business Centra RA',
    items:[{qty:39,pack:12,uop:'CS',desc:'Cafe Molido Andatti 250gr',item:'7501954906644',dept:623,cost:1221.60,ext:47642.40},
    {qty:76,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 50 g',item:'7501954908600',dept:623,cost:448.80,ext:34108.80},
    {qty:72,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 100 g',item:'7501954908617',dept:623,cost:785.40,ext:56548.80},
    {qty:108,pack:60,uop:'CS',desc:'Cafe soluble andatti Sachet 35 g',item:'7501954909409',dept:623,cost:522.00,ext:56376.00},
    {qty:38,pack:12,uop:'CS',desc:'Cafe soluble descafeinado andatti 100g',item:'7501954910016',dept:623,cost:943.68,ext:35859.84},
    {qty:18,pack:80,uop:'CS',desc:'Capuchino clasico andatti 25gr',item:'7501954910214',dept:623,cost:580.19,ext:10443.46},
    {qty:6,pack:80,uop:'CS',desc:'Chocolate clasico andatti 25g',item:'7501954910238',dept:1188,cost:580.80,ext:3484.80},
    {qty:71,pack:60,uop:'CS',desc:'Cafe soluble descaf andatti Sachet 35g',item:'7501954910344',dept:623,cost:542.40,ext:38510.40},
    {qty:9,pack:12,uop:'CS',desc:'Cafe molido descafeinado andatti 250gr',item:'7502271151212',dept:623,cost:1368.24,ext:12314.16},
    {qty:27,pack:12,uop:'CS',desc:'Cafe andatti soluble descafeinado 50g',item:'7502271151601',dept:623,cost:524.04,ext:14149.08},
    {qty:5,pack:80,uop:'CS',desc:'Capuchino descafeinado andatti 25gr',item:'7502271152448',dept:623,cost:580.19,ext:2900.96},
    {qty:19,pack:80,uop:'CS',desc:'Sachet andatti capuchino vainilla 25gr',item:'7502271152455',dept:623,cost:580.19,ext:11023.65},
    {qty:73,pack:9,uop:'CS',desc:'Cafe Soluble Andatti 275g',item:'7502271155920',dept:623,cost:1215.72,ext:88747.56},
    {qty:20,pack:80,uop:'CS',desc:'Sachet andatti capuchino Moka 25gr',item:'7502271159577',dept:623,cost:580.19,ext:11603.84},
    {qty:10,pack:9,uop:'CS',desc:'Cafe Soluble Andatti Descafeinado 275g',item:'7502294221763',dept:623,cost:1467.63,ext:14676.30},
    {qty:17,pack:80,uop:'CS',desc:'Sachet andatti capuchino Canela 25g',item:'7502294223750',dept:623,cost:580.19,ext:9863.26},
    {qty:10,pack:80,uop:'CS',desc:'Sachet andatti capuchino Caramelo 25g',item:'7502294223767',dept:623,cost:580.19,ext:5801.92},
    {qty:5,pack:80,uop:'CS',desc:'CAPUCHINO FRIO VAINILLA SACHET 25 G.',item:'7502294225785',dept:623,cost:642.04,ext:3210.20},
    {qty:5,pack:80,uop:'CS',desc:'CAPUCHINO FRIO MOKA SACHET 25 G.',item:'7502294225792',dept:623,cost:642.04,ext:3210.20},
    {qty:6,pack:80,uop:'CS',desc:'CAPUCHINO AVELLANAS ANDATTI 25G',item:'7502294228007',dept:623,cost:642.04,ext:3852.24}]
  },
  'po-gua':{
    id:'po-gua',orderNo:'76933175',site:'SERVICIOS ADMINISTRATIVOS 15GUA 69098',
    file:'76933175_FA69098_04142026_SERVICIOS_ADMINISTRATIVOS_15GUA.pdf',
    vendor:'101041',contact:'PRECIADO NORA',phone:'6622890740',fax:'66-22890740',
    notAfter:'21-Apr-2026',notBefore:'14-Apr-2026',terms:'30 dias',discount:'0.00',
    total:'581,443.84',location:'Tlajomulco / GDL',
    shipTo:'Tlajomulco de Zuniga JAL 45640',addr:'Av. Pedro Parra Centeno 1800\nEntre Sta Cruz y Av. Vista Sur',
    items:[{qty:46,pack:12,uop:'CS',desc:'Cafe Molido Andatti 250gr',item:'7501954906644',dept:623,cost:1221.60,ext:56193.60},
    {qty:81,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 50 g',item:'7501954908600',dept:623,cost:448.80,ext:36352.80},
    {qty:92,pack:12,uop:'CS',desc:'Cafe soluble andatti Frasco 100 g',item:'7501954908617',dept:623,cost:785.40,ext:72256.80},
    {qty:159,pack:60,uop:'CS',desc:'Cafe soluble andatti Sachet 35 g',item:'7501954909409',dept:623,cost:522.00,ext:82998.00},
    {qty:15,pack:12,uop:'CS',desc:'Cafe soluble descafeinado andatti 100g',item:'7501954910016',dept:623,cost:943.68,ext:14155.20},
    {qty:16,pack:80,uop:'CS',desc:'Capuchino clasico andatti 25gr',item:'7501954910214',dept:623,cost:580.19,ext:9283.07},
    {qty:14,pack:80,uop:'CS',desc:'Chocolate clasico andatti 25g',item:'7501954910238',dept:1188,cost:580.80,ext:8131.20},
    {qty:38,pack:60,uop:'CS',desc:'Cafe soluble descaf andatti Sachet 35g',item:'7501954910344',dept:623,cost:542.40,ext:20611.20},
    {qty:14,pack:12,uop:'CS',desc:'Cafe molido descafeinado andatti 250gr',item:'7502271151212',dept:623,cost:1368.24,ext:19155.36},
    {qty:36,pack:12,uop:'CS',desc:'Cafe andatti soluble descafeinado 50g',item:'7502271151601',dept:623,cost:524.04,ext:18865.44},
    {qty:8,pack:80,uop:'CS',desc:'Capuchino descafeinado andatti 25gr',item:'7502271152448',dept:623,cost:580.19,ext:4641.54},
    {qty:25,pack:80,uop:'CS',desc:'Sachet andatti capuchino vainilla 25gr',item:'7502271152455',dept:623,cost:580.19,ext:14504.80},
    {qty:123,pack:9,uop:'CS',desc:'Cafe Soluble Andatti 275g',item:'7502271155920',dept:623,cost:1215.72,ext:149533.56},
    {qty:29,pack:80,uop:'CS',desc:'Sachet andatti capuchino Moka 25gr',item:'7502271159577',dept:623,cost:580.19,ext:16825.57},
    {qty:2,pack:9,uop:'CS',desc:'Cafe Soluble Andatti Descafeinado 275g',item:'7502294221763',dept:623,cost:1467.63,ext:2935.26},
    {qty:24,pack:80,uop:'CS',desc:'Sachet andatti capuchino Canela 25g',item:'7502294223750',dept:623,cost:580.19,ext:13924.61},
    {qty:21,pack:80,uop:'CS',desc:'Sachet andatti capuchino Caramelo 25g',item:'7502294223767',dept:623,cost:580.19,ext:12184.03},
    {qty:14,pack:80,uop:'CS',desc:'CAPUCHINO FRIO REGULAR SACHET 25 G.',item:'7502294225778',dept:623,cost:642.04,ext:8988.56},
    {qty:13,pack:80,uop:'CS',desc:'CAPUCHINO FRIO VAINILLA SACHET 25 G.',item:'7502294225785',dept:623,cost:642.04,ext:8346.52},
    {qty:12,pack:80,uop:'CS',desc:'CAPUCHINO FRIO MOKA SACHET 25 G.',item:'7502294225792',dept:623,cost:642.04,ext:7704.48},
    {qty:6,pack:80,uop:'CS',desc:'CAPUCHINO AVELLANAS ANDATTI 25G',item:'7502294228007',dept:623,cost:642.04,ext:3852.24}]
  }
};

const emailsData=[

/* ══════════════ em-po-all · RESUMEN + 6 OCs ══════════════ */
{
  id:'em-po-all',
  subject:'RV: Pedidos OXXO marca propia — SERVICIOS ADMINISTRATIVOS — Carga Masiva Semanal',
  from:'Rommel Gil Vera',fromName:'Rommel Gil Vera',fromEmail:'rommel.gil.vera@emeal.nttdata.com',
  date:'Lun 14 Abr 2026',time:'08:32',
  preview:'Buen día, se adjuntan las 6 Órdenes de Compra FEMSA Comercio y el Resumen ejecutivo...',
  tag:'oc',priority:'high',read:false,backlogRef:'b-0001',
  oraclePOId:'po-agu',
  area:'Multi-Zona',poNumber:'76933176 / 72 / 73 / 65 / 70 / 75',
  attachments:[
    {name:'RESUMEN_OC_SERVICIOS_ADIMINISTRATIVOS_2026.xlsx',type:'xlsx',size:'2.9 MB'},
    {name:'76933176_FA216510_04142026_SERVICIOS_ADMINISTRATIVOS_15AGU-.pdf',type:'pdf',size:'26.7 KB',poRef:'po-agu'},
    {name:'76933072_FA30481_04142026_SERVICIOS_ADMINISTRATIVOS_15TQV.pdf',type:'pdf',size:'27.1 KB',poRef:'po-tqv'},
    {name:'76933173_FA45858_04142026_SERVICIOS_ADMINISTRATIVOS_15VCZ.pdf',type:'pdf',size:'26.8 KB',poRef:'po-vcz'},
    {name:'76933065_FA11309_04142026_SERVICIOS_ADMINISTRATIVOS_15OBQ.pdf',type:'pdf',size:'27.1 KB',poRef:'po-obq'},
    {name:'76933070_FA20557_04142026_SERVICIOS_ADMINISTRATIVOS_15VHD-.pdf',type:'pdf',size:'27.0 KB',poRef:'po-vhd'},
    {name:'76933175_FA69098_04142026_SERVICIOS_ADMINISTRATIVOS_15GUA.pdf',type:'pdf',size:'27.1 KB',poRef:'po-gua'}
  ],
  body:'De: Sistema Oracle Retail — FEMSA Comercio <ordrpt@femsa-comercio.com.mx>\nPara: pedidos@caffenio.com; rommel.gil.vera@emeal.nttdata.com\nAsunto: Pedidos OXXO marca propia — SERVICIOS ADMINISTRATIVOS — Carga Masiva RMS\nFecha: Lunes, 14 de abril de 2026 07:58\n\n──────────────────────────────────────────────────────────────\nREPORTE AUTOMÁTICO — ORACLE RETAIL (ORD_DET) — FEMSA COMERCIO\n──────────────────────────────────────────────────────────────\n\nBuen día equipo Caffenio,\n\nSe generaron 6 Órdenes de Compra mediante el sistema Oracle Retail (FEMSA Comercio) para la semana del 14 al 22 de abril de 2026.\n\nVENDOR: 101041 — SERVICIOS ADMINISTRATIVOS\nCONTACTO: PRECIADO NORA | TEL: 6622890740 | FAX: 66-22890740\nCOMENTARIOS: Carga Masiva RMS | TÉRMINOS: 30 días | DIVISA: MXN\n\n┌─────────────────────────────────────────────────────────┐\n│  OC            DESTINO              TOTAL MXN   VENCE   │\n│  76933176      Aguascalientes      143,544.11   22-Abr  │\n│  76933072      Querétaro           348,257.85   20-Abr  │\n│  76933173      Veracruz            300,534.58   21-Abr  │\n│  76933065      Ciudad Obregón      533,410.72   21-Abr  │\n│  76933070      Villahermosa        464,327.87   22-Abr  │\n│  76933175      Tlajomulco / GDL    581,443.84   21-Abr  │\n│  ────────────────────────────────────────────────────── │\n│  TOTAL 6 OCs                     2,371,518.97           │\n└─────────────────────────────────────────────────────────┘\n\nSe adjuntan los reportes individuales PDF (ORD_DET) y el resumen ejecutivo en Excel.\n\n⚠  IMPORTANTE: Para entrega en CD es obligatorio zapato con casquillo de acero.\nFavor confirmar cita de entrega en las próximas 48 horas.\n\nQuedo al pendiente,\nRommel Gil Vera | NTT Data\nOn behalf of OXXO / FEMSA Comercio'
},

/* ══════════════ em001 · GUA Tlajomulco — OC más grande ══════════════ */
{
  id:'em001',
  subject:'RV: OC FEMSA 76933175 — Tlajomulco/GDL [Vigencia 21-Abr]',
  from:'OXXO Compras',fromName:'OXXO Compras Jalisco',fromEmail:'compras.jal@oxxo.com',
  date:'Lun 14 Abr 2026',time:'09:10',
  preview:'OC 76933175 — $581,443.84 MXN — Requerimiento Tlajomulco. Por favor confirmar recepción...',
  tag:'oc',priority:'high',read:false,backlogRef:'b-0002',
  oraclePOId:'po-gua',area:'15GUA',poNumber:'76933175',
  attachments:[
    {name:'76933175_FA69098_04142026_SERVICIOS_ADMINISTRATIVOS_15GUA.pdf',type:'pdf',size:'27.1 KB',poRef:'po-gua'}
  ],
  body:'De: OXXO Compras Jalisco <compras.jal@oxxo.com>\nPara: pedidos@caffenio.com\nCC: rommel.gil.vera@emeal.nttdata.com\nAsunto: OC FEMSA 76933175 — Tlajomulco / GDL\nFecha: Lunes, 14 de abril de 2026 09:10\n\nBuen día,\n\nSe adjunta la Orden de Compra No. 76933175 para el sitio Tlajomulco (SERVICIOS ADMINISTRATIVOS 15GUA).\n\nDETALLE OC:\n  • No. Orden:     76933175\n  • Vendor Site:   15GUA — 69098\n  • Ship To:       Tlajomulco de Zuniga, JAL 45640\n  • No. Antes de:  21-Abr-2026\n  • Total MXN:     $581,443.84\n  • Producto top:  Cafe Soluble Andatti 275g (123 CS — $149,533.56)\n\nFavor confirmar disponibilidad de stock y fecha de entrega.\n\nSaludos,\nOXXO Compras Jalisco'
},

/* ══════════════ em002 · OBQ Obregón ══════════════ */
{
  id:'em002',
  subject:'RV: OC FEMSA 76933065 — Cd. Obregón [⚠ Vence 21-Abr]',
  from:'OXXO Compras Noreste',fromName:'OXXO Compras Noreste',fromEmail:'compras.ne@oxxo.com',
  date:'Lun 14 Abr 2026',time:'09:45',
  preview:'URGENTE — OC 76933065 Ciudad Obregón $533,410.72. Vence 21-Abr, confirmar cita entrega...',
  tag:'urgente',priority:'high',read:false,backlogRef:'b-0003',
  oraclePOId:'po-obq',area:'15OBQ',poNumber:'76933065',
  attachments:[
    {name:'76933065_FA11309_04142026_SERVICIOS_ADMINISTRATIVOS_15OBQ.pdf',type:'pdf',size:'27.1 KB',poRef:'po-obq'}
  ],
  body:'De: OXXO Compras Noreste <compras.ne@oxxo.com>\nPara: pedidos@caffenio.com\nAsunto: OC FEMSA 76933065 — Ciudad Obregón [URGENTE]\nFecha: Lunes, 14 de abril de 2026 09:45\n\n⚠ URGENTE — Vence 21 de abril de 2026\n\nOC No. 76933065 para el Parque Industrial de Obregón:\n\n  • Vendor Site:   15OBQ — 11309\n  • Ship To:       Calzada Fco Villanueva Castelo #2054, SON 85050\n  • Total MXN:     $533,410.72\n  • No. Antes de:  21-Abr-2026 ← PLAZO AJUSTADO\n  • Producto top:  Cafe Soluble Andatti 275g (99 CS — $120,356.28)\n\nSolicito confirmación de cita de entrega a más tardar mañana martes 15 de abril.\n\nSaludos,\nOXXO Compras Noreste'
},

/* ══════════════ em003 · VHD Villahermosa ══════════════ */
{
  id:'em003',
  subject:'RV: OC FEMSA 76933070 — Villahermosa',
  from:'OXXO Compras Sur',fromName:'OXXO Compras Sureste',fromEmail:'compras.sur@oxxo.com',
  date:'Lun 14 Abr 2026',time:'10:18',
  preview:'OC 76933070 Villahermosa $464,327.87 — Tabasco Business Center...',
  tag:'oc',priority:'normal',read:true,
  oraclePOId:'po-vhd',area:'15VHD',poNumber:'76933070',
  attachments:[
    {name:'76933070_FA20557_04142026_SERVICIOS_ADMINISTRATIVOS_15VHD-.pdf',type:'pdf',size:'27.0 KB',poRef:'po-vhd'}
  ],
  body:'De: OXXO Compras Sureste <compras.sur@oxxo.com>\nPara: pedidos@caffenio.com\nAsunto: OC FEMSA 76933070 — Villahermosa\nFecha: Lunes, 14 de abril de 2026 10:18\n\nBuen día,\n\nOC No. 76933070 para el sitio Villahermosa (SERVICIOS ADMINISTRATIVOS 15VHD).\n\n  • Vendor Site:   15VHD — 20557\n  • Ship To:       Circuito Tabasco Pte MZA 5, Cunduacan TAB 8669\n  • Total MXN:     $464,327.87\n  • No. Antes de:  22-Abr-2026\n  • Producto top:  Cafe Soluble Andatti 275g (73 CS — $88,747.56)\n\nQuedamos en espera de confirmación.\n\nSaludos,\nOXXO Compras Sureste'
},

/* ══════════════ em004 · TQV Querétaro ══════════════ */
{
  id:'em004',
  subject:'RV: OC FEMSA 76933072 — Querétaro',
  from:'OXXO Compras Centro',fromName:'OXXO Compras Centro',fromEmail:'compras.cen@oxxo.com',
  date:'Lun 14 Abr 2026',time:'11:05',
  preview:'OC 76933072 Querétaro $348,257.85. Vence 20-Abr. Requerimiento: Cafe Soluble Andatti 275g...',
  tag:'oc',priority:'normal',read:true,
  oraclePOId:'po-tqv',area:'15TQV',poNumber:'76933072',
  attachments:[
    {name:'76933072_FA30481_04142026_SERVICIOS_ADMINISTRATIVOS_15TQV.pdf',type:'pdf',size:'27.1 KB',poRef:'po-tqv'}
  ],
  body:'De: OXXO Compras Centro <compras.cen@oxxo.com>\nPara: pedidos@caffenio.com\nAsunto: OC FEMSA 76933072 — Querétaro\nFecha: Lunes, 14 de abril de 2026 11:05\n\nBuen día equipo Caffenio,\n\nOC No. 76933072 para el sitio Querétaro (SERVICIOS ADMINISTRATIVOS 15TQV).\n\n  • Vendor Site:   15TQV — 30481\n  • Ship To:       Av. Industria Minera 501, QRO 76000\n  • Total MXN:     $348,257.85\n  • No. Antes de:  20-Abr-2026\n  • Producto top:  Cafe Soluble Andatti 275g (60 CS — $72,943.20)\n\nFavor confirmar.\n\nSaludos,\nOXXO Compras Centro'
},

/* ══════════════ em005 · VCZ Veracruz ══════════════ */
{
  id:'em005',
  subject:'RV: OC FEMSA 76933173 — Veracruz',
  from:'OXXO Compras Golfo',fromName:'OXXO Compras Golfo',fromEmail:'compras.golf@oxxo.com',
  date:'Lun 14 Abr 2026',time:'11:42',
  preview:'OC 76933173 Veracruz $300,534.58. Café Sachet 35g mayor volumen esta semana...',
  tag:'oc',priority:'normal',read:true,
  oraclePOId:'po-vcz',area:'15VCZ',poNumber:'76933173',
  attachments:[
    {name:'76933173_FA45858_04142026_SERVICIOS_ADMINISTRATIVOS_15VCZ.pdf',type:'pdf',size:'26.8 KB',poRef:'po-vcz'}
  ],
  body:'De: OXXO Compras Golfo <compras.golf@oxxo.com>\nPara: pedidos@caffenio.com\nAsunto: OC FEMSA 76933173 — Veracruz\nFecha: Lunes, 14 de abril de 2026 11:42\n\nBuen día,\n\nOC No. 76933173 para el sitio Veracruz (SERVICIOS ADMINISTRATIVOS 15VCZ).\n\n  • Vendor Site:   15VCZ — 45858\n  • Ship To:       Boca del Río, VER 91700\n  • Total MXN:     $300,534.58\n  • No. Antes de:  21-Abr-2026\n  • Producto top:  Cafe soluble andatti Sachet 35g (112 CS — $58,464.00)\n\nSaludos,\nOXXO Compras Golfo'
},

/* ══════════════ em006 · AGU Aguascalientes ══════════════ */
{
  id:'em006',
  subject:'RV: OC FEMSA 76933176 — Aguascalientes',
  from:'OXXO Compras Occidente',fromName:'OXXO Compras Occidente',fromEmail:'compras.occ@oxxo.com',
  date:'Lun 14 Abr 2026',time:'12:15',
  preview:'OC 76933176 Aguascalientes $143,544.11. Volumen menor. Vence 22-Abr...',
  tag:'oc',priority:'normal',read:true,
  oraclePOId:'po-agu',area:'15AGU',poNumber:'76933176',
  attachments:[
    {name:'76933176_FA216510_04142026_SERVICIOS_ADMINISTRATIVOS_15AGU-.pdf',type:'pdf',size:'26.7 KB',poRef:'po-agu'}
  ],
  body:'De: OXXO Compras Occidente <compras.occ@oxxo.com>\nPara: pedidos@caffenio.com\nAsunto: OC FEMSA 76933176 — Aguascalientes\nFecha: Lunes, 14 de abril de 2026 12:15\n\nBuen día,\n\nOC No. 76933176 para el sitio Aguascalientes (SERVICIOS ADMINISTRATIVOS 15AGU).\n\n  • Vendor Site:   15AGU — 216510\n  • Ship To:       Blvd. Aguascalientes Sur 3603, AGS 20230\n  • Total MXN:     $143,544.11\n  • No. Antes de:  22-Abr-2026\n  • Producto top:  Cafe Soluble Andatti 275g (14 CS — $17,020.08)\n\nSaludos,\nOXXO Compras Occidente'
},

/* ══════════════ em007 · Resumen Excel ══════════════ */
{
  id:'em007',
  subject:'Resumen Ejecutivo OCs — SERVICIOS ADMINISTRATIVOS — Semana 16/2026',
  from:'Rommel Gil Vera',fromName:'Rommel Gil Vera',fromEmail:'rommel.gil.vera@emeal.nttdata.com',
  date:'Lun 14 Abr 2026',time:'13:00',
  preview:'Comparto el resumen ejecutivo consolidado de las 6 OCs Semana 16. Total: $2,371,518.97 MXN...',
  tag:'resumen',priority:'normal',read:true,
  area:'Multi-Zona',poNumber:'Semana 16/2026',
  attachments:[
    {name:'RESUMEN_OC_SERVICIOS_ADIMINISTRATIVOS_2026.xlsx',type:'xlsx',size:'2.9 MB'}
  ],
  body:'De: Rommel Gil Vera <rommel.gil.vera@emeal.nttdata.com>\nPara: operaciones@caffenio.com\nCC: pedidos@caffenio.com\nAsunto: Resumen Ejecutivo OCs — SERVICIOS ADMINISTRATIVOS — Semana 16/2026\nFecha: Lunes, 14 de abril de 2026 13:00\n\nBuenas tardes equipo,\n\nComparto el resumen ejecutivo consolidado de las Órdenes de Compra de la semana 16/2026 para OXXO — SERVICIOS ADMINISTRATIVOS.\n\nCONSOLIDADO SEMANA 16:\n  6 OCs procesadas | $2,371,518.97 MXN total\n\n  Aguascalientes (AGU)  $143,544.11\n  Querétaro (TQV)       $348,257.85\n  Veracruz (VCZ)        $300,534.58\n  Cd. Obregón (OBQ)     $533,410.72\n  Villahermosa (VHD)    $464,327.87\n  Tlajomulco/GDL (GUA)  $581,443.84\n\nSe adjunta el Excel con el detalle completo por SKU y zona.\n\nRommel Gil Vera | NTT Data\nProyecto McKinsey — OXXO / FEMSA Comercio'
},

/* ══════════════ error-email ══════════════ */
{
  id:'e-0001',
  subject:'⚠ ERROR SAP: OC 76933065 — Material PKG-602 no encontrado',
  from:'SAP Sistema',fromName:'SAP Sistema CAF1',fromEmail:'sap-noreply@caffenio.com',
  date:'Lun 14 Abr 2026',time:'14:32',
  preview:'BAPI_SALESORDER_CREATEFROMDAT2 falló. Material PKG-602 no existe en el mandante CAF...',
  tag:'error',priority:'high',read:false,errorRef:'e-0001',
  area:'15OBQ',poNumber:'76933065',
  attachments:[],
  body:'De: SAP Sistema CAF1 <sap-noreply@caffenio.com>\nPara: operaciones@caffenio.com\nAsunto: ERROR SAP — OC 76933065 — Material no encontrado\nFecha: Lunes, 14 de abril de 2026 14:32\n\n⚠ ERROR EN PROCESAMIENTO AUTOMÁTICO\n\nFunción:  BAPI_SALESORDER_CREATEFROMDAT2\nMandante: CAF\nOC:       76933065 — SERVICIOS ADMINISTRATIVOS 15OBQ\nItem:     PKG-602 (Tapa Vaso 16oz)\n\nMensaje SAP:\n  Material PKG-602 does not exist in plant CAF1 (MSGID: M3, MSG: 002)\n\nAcción requerida:\n  1. Verificar maestro de materiales en MM03 (PKG-602 / CAF1)\n  2. Si el material no existe, crear en MM01 con tipo FERT\n  3. Re-ejecutar la orden desde el AI Control Tower\n\nAtención: La OC 76933065 ($533,410.72) queda en estado BLOQUEADO hasta resolución.'
}
  ];
  // Also add error email to backlog refs
  const backlogRefs={
    'b-0001':'em-po-all',
    'b-0002':'em001',
    'b-0003':'em002',
    'e-0001':'e-0001'
  };

const oraclePOs = ORACLE_PO_DATA;
let activeEmailId = null;
let activeObsAgent = 'ag01';

function renderRepositorio(){
  filterRepoDocs('');
}

function filterRepoDocs(q){
  const typeF = document.getElementById('repo-filter-type').value;
  const statusF = document.getElementById('repo-filter-status').value;
  const search = (q || document.getElementById('repo-search-input').value || '').toLowerCase();
  const filtered = repoDocs.filter(d => {
    const matchQ = !search || d.name.toLowerCase().includes(search) || d.client.toLowerCase().includes(search) || d.poNum.toLowerCase().includes(search) || d.area.toLowerCase().includes(search);
    const matchType = typeF === 'all' || d.type === typeF;
    const matchStatus = statusF === 'all' || d.status === statusF;
    return matchQ && matchType && matchStatus;
  });
  const grid = document.getElementById('repo-grid');
  if(!grid) return;
  if(!filtered.length){
    grid.innerHTML = '<div style="grid-column:1/-1;padding:60px;text-align:center;color:var(--sub);">No se encontraron documentos.</div>';
    return;
  }
  grid.innerHTML = filtered.map(d => {
    const icon = d.type==='xlsx'?'📊':d.type==='pdf'?'📄':'📧';
    const previewClass = `repo-doc-preview-${d.type}`;
    return `
      <div class="repo-doc-card" onclick="openDocumentPDF('${d.id}')">
        <div class="repo-doc-preview ${previewClass}">
          <div style="font-size:44px;filter:drop-shadow(0 2px 4px rgba(0,0,0,.15));">${icon}</div>
          <div class="repo-doc-preview-lines">
            <div class="repo-doc-preview-line" style="width:90%;"></div>
            <div class="repo-doc-preview-line" style="width:70%;"></div>
            <div class="repo-doc-preview-line" style="width:80%;"></div>
            <div class="repo-doc-preview-line" style="width:60%;"></div>
          </div>
        </div>
        <div class="repo-doc-card-body">
          <div class="repo-doc-name" title="${d.name}">${d.name}</div>
          <div class="repo-doc-meta">
            <span>${d.size} · ${d.date}</span>
            <span style="font-family:var(--mono);font-size:10.5px;">${d.type.toUpperCase()}</span>
          </div>
          <div class="repo-doc-tags">
            <span class="repo-doc-tag repo-doc-tag-${d.type}">${d.type.toUpperCase()}</span>
            ${d.poNum!=='—'?`<span class="repo-doc-tag repo-doc-tag-po">OC</span>`:''}
            <span class="repo-doc-tag repo-doc-tag-${d.status}">${d.status==='proc'?'✓ Procesado':'⏳ Pendiente'}</span>
          </div>
          <div style="font-size:11px;color:var(--sub);margin-bottom:10px;line-height:1.5;">
            ${d.desc||''}
          </div>
        </div>
      </div>
    `;
  }).join('');
}

function openOraclePO(poId){
  const po=ORACLE_PO_DATA[poId]; if(!po) return;

  const fmtNum = n => n.toLocaleString('en-MX',{minimumFractionDigits:2,maximumFractionDigits:2});

  // ── item rows ──────────────────────────────────────────────────────────────
  const rowsHtml = po.items.map((it,i)=>`
    <tr style="background:${i%2===0?'white':'#F8FAFB'};">
      <td style="border:1px solid #D0DCE8;padding:4px 8px;text-align:center;font-size:11.5px;font-weight:700;">${it.qty}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 8px;text-align:center;font-size:11.5px;">${it.pack}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 8px;text-align:center;font-size:11.5px;">${it.uop}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 10px;font-size:11.5px;">${it.desc}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 8px;text-align:center;font-size:10.5px;color:#555;">${it.item}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 8px;text-align:center;font-size:11.5px;">${it.dept}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 10px;text-align:right;font-size:11.5px;">${fmtNum(it.cost)}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 10px;text-align:right;font-size:11.5px;font-weight:700;">${fmtNum(it.ext)}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 10px;text-align:right;font-size:11.5px;font-weight:700;">${fmtNum(it.ext)}</td>
    </tr>`).join('');

  // ── summary rows ───────────────────────────────────────────────────────────
  const summaryHtml = po.items.map((it,i)=>`
    <tr style="background:${i%2===0?'white':'#F8FAFB'};">
      <td style="border:1px solid #D0DCE8;padding:4px 8px;text-align:center;font-size:11.5px;font-weight:700;">${it.qty}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 8px;text-align:center;font-size:11.5px;">${it.pack}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 8px;text-align:center;font-size:11.5px;">${it.uop}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 8px;font-size:9px;color:#888;">—</td>
      <td style="border:1px solid #D0DCE8;padding:4px 10px;font-size:11.5px;">${it.desc}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 10px;text-align:right;font-size:11.5px;font-weight:700;">${fmtNum(it.ext)}</td>
      <td style="border:1px solid #D0DCE8;padding:4px 10px;text-align:right;font-size:11.5px;font-weight:700;">${fmtNum(it.ext)}</td>
    </tr>`).join('');

  // ── Oracle Retail PO HTML ──────────────────────────────────────────────────
  const addrLines = (po.addr||'').replace(/\\n/g,'<br>');
  const shipLines = (po.shipTo||'').replace(/,/g,'<br>');

  const poHtml=`
<div style="font-family:Arial,sans-serif;font-size:12px;background:white;color:#111;max-width:100%;margin:0;padding:0;">

  <!-- ── PAGE 1: Cover ── -->
  <div style="border:1px solid #bbb;margin-bottom:12px;background:white;">
    <!-- Oracle header -->
    <div style="display:flex;align-items:center;justify-content:space-between;padding:8px 14px;border-bottom:1px solid #ccc;">
      <div style="font-size:18px;font-weight:900;letter-spacing:-1px;">
        <span style="color:#CC0000;">ORACLE</span><span style="color:#336699;font-weight:400;"> Retail</span>
      </div>
      <div style="text-align:center;flex:1;padding:0 20px;">
        <div style="font-size:15px;font-weight:700;">Purchase Order Report</div>
        <div style="font-size:12px;font-weight:700;">Order No: ${po.orderNo}</div>
        <div style="font-size:12px;color:#555;">FEMSA Comercio</div>
      </div>
      <div style="text-align:right;font-size:11px;color:#555;">
        <div>Report Date: 14-Apr-26</div>
        <div>Report: (ORD_DET)</div>
        <div>Page: 1 OF 5</div>
      </div>
    </div>

    <!-- Blue vendor header -->
    <table width="100%" cellpadding="6" cellspacing="0" style="background:#7AAFC0;color:#000;border-collapse:collapse;font-size:11.5px;">
      <tr>
        <td width="15%" style="font-weight:700;text-align:right;padding-right:6px;">BUYER:</td><td colspan="3"></td>
        <td style="font-weight:700;text-align:right;padding-right:6px;">NOT AFTER DATE:</td><td style="font-weight:700;">${po.notAfter}</td>
      </tr>
      <tr>
        <td style="font-weight:700;text-align:right;padding-right:6px;">PHONE:</td><td></td>
        <td style="font-weight:700;text-align:right;padding-right:6px;">FAX:</td><td></td>
        <td style="font-weight:700;text-align:right;padding-right:6px;">NOT BEFORE DATE:</td><td style="font-weight:700;">${po.notBefore}</td>
      </tr>
      <tr>
        <td style="font-weight:700;text-align:right;padding-right:6px;">VENDOR:</td><td colspan="3">${po.vendor}</td><td></td><td></td>
      </tr>
      <tr>
        <td style="font-weight:700;text-align:right;padding-right:6px;">VENDOR SITE:</td>
        <td colspan="2">${po.site}</td>
        <td></td>
        <td style="font-weight:700;text-align:right;padding-right:6px;">TERMS:</td><td>${po.terms}</td>
      </tr>
      <tr>
        <td></td><td colspan="2" style="font-size:10.5px;">${addrLines}</td><td></td>
        <td style="font-weight:700;text-align:right;padding-right:6px;">DISCOUNT % APPLIED:</td><td>${po.discount}</td>
      </tr>
      <tr>
        <td style="font-weight:700;text-align:right;padding-right:6px;">CONTACT:</td><td colspan="2">${po.contact}</td>
        <td></td>
        <td colspan="2" style="font-weight:700;">PO TOTAL COST</td>
      </tr>
      <tr>
        <td style="font-weight:700;text-align:right;padding-right:6px;">PHONE:</td><td>${po.phone}</td>
        <td style="font-weight:700;text-align:right;padding-right:6px;">FAX:</td><td>${po.fax}</td>
        <td style="font-weight:700;text-align:right;padding-right:6px;">NET OF DISCOUNT:</td><td style="font-weight:900;">${po.total}</td>
      </tr>
      <tr>
        <td></td><td></td><td></td><td></td>
        <td style="font-weight:700;text-align:right;padding-right:6px;">ORDER CURRENCY:</td><td>MXN</td>
      </tr>
      <tr>
        <td style="font-weight:700;text-align:right;padding-right:6px;">FREIGHT TERMS:</td><td colspan="5"></td>
      </tr>
      <tr>
        <td style="font-weight:700;text-align:right;padding-right:6px;">FOB TERMS PAY METHOD:</td><td colspan="5"></td>
      </tr>
      <tr>
        <td style="font-weight:700;text-align:right;padding-right:6px;">TRANS. RESPONSIBILITY:</td><td colspan="5"></td>
      </tr>
      <tr>
        <td style="font-weight:700;text-align:right;padding-right:6px;">COMMENTS:</td>
        <td colspan="5">Carga Masiva RMS</td>
      </tr>
    </table>
  </div>

  <!-- ── PAGE 2: Ship-To + Items ── -->
  <div style="border:1px solid #bbb;margin-bottom:12px;background:white;">
    <!-- header repeat -->
    <div style="display:flex;align-items:center;justify-content:space-between;padding:6px 14px;border-bottom:1px solid #ccc;background:#FAFAFA;">
      <div style="font-size:16px;font-weight:900;"><span style="color:#CC0000;">ORACLE</span><span style="color:#336699;font-weight:400;"> Retail</span></div>
      <div style="text-align:center;flex:1;">
        <div style="font-size:13px;font-weight:700;">Purchase Order Report</div>
        <div style="font-size:11px;">Order No: ${po.orderNo} — FEMSA Comercio</div>
      </div>
      <div style="font-size:10.5px;color:#555;text-align:right;">Report Date: 14-Apr-26<br>Page: 2 OF 5</div>
    </div>

    <!-- Ship-to blue table -->
    <table width="100%" cellpadding="5" cellspacing="0" style="background:#7AAFC0;border-collapse:collapse;font-size:11.5px;">
      <tr>
        <td width="15%" style="font-weight:700;text-align:right;">SHIP TO:</td>
        <td colspan="2"><strong>${po.location}</strong><br><span style="font-size:10.5px;">${addrLines}</span><br>${shipLines}</td>
        <td width="30%" style="font-weight:700;">PO COST PER STORE<br>NET OF DISCOUNT: 0.00<br>ORDER CURRENCY: MXN</td>
      </tr>
      <tr><td style="font-weight:700;text-align:right;">MANAGER:</td><td></td><td></td><td></td></tr>
      <tr><td style="font-weight:700;text-align:right;">PHONE:</td><td></td><td style="font-weight:700;text-align:right;">FAX:</td><td></td></tr>
    </table>

    <!-- Items table -->
    <table width="100%" cellpadding="0" cellspacing="0" style="border-collapse:collapse;margin-top:0;">
      <thead>
        <tr style="background:#4C8FC0;color:white;">
          <th style="padding:5px 8px;text-align:center;font-size:11px;border:1px solid #2A6090;white-space:nowrap;">QUANTITY<br>ORDERED</th>
          <th style="padding:5px 8px;text-align:center;font-size:11px;border:1px solid #2A6090;">PACK SIZE</th>
          <th style="padding:5px 8px;text-align:center;font-size:11px;border:1px solid #2A6090;">UOP</th>
          <th style="padding:5px 10px;font-size:11px;border:1px solid #2A6090;">DESCRIPTION</th>
          <th style="padding:5px 8px;text-align:center;font-size:11px;border:1px solid #2A6090;">ITEM</th>
          <th style="padding:5px 8px;text-align:center;font-size:11px;border:1px solid #2A6090;">DEPT</th>
          <th style="padding:5px 10px;text-align:right;font-size:11px;border:1px solid #2A6090;white-space:nowrap;">NET UOP COST</th>
          <th style="padding:5px 10px;text-align:right;font-size:11px;border:1px solid #2A6090;white-space:nowrap;">VENDOR<br>EXT.COST</th>
          <th style="padding:5px 10px;text-align:right;font-size:11px;border:1px solid #2A6090;white-space:nowrap;">NET<br>EXT. COST</th>
        </tr>
      </thead>
      <tbody>${rowsHtml}</tbody>
    </table>
  </div>

  <!-- ── PAGE 4: Summary ── -->
  <div style="border:1px solid #bbb;margin-bottom:12px;background:white;">
    <div style="display:flex;align-items:center;justify-content:space-between;padding:6px 14px;border-bottom:1px solid #ccc;background:#FAFAFA;">
      <div style="font-size:16px;font-weight:900;"><span style="color:#CC0000;">ORACLE</span><span style="color:#336699;font-weight:400;"> Retail</span></div>
      <div style="text-align:center;flex:1;"><div style="font-size:13px;font-weight:700;">Purchase Order Report</div><div style="font-size:11px;">Order No: ${po.orderNo} — FEMSA Comercio</div></div>
      <div style="font-size:10.5px;color:#555;text-align:right;">Report Date: 14-Apr-26<br>Page: 4 OF 5</div>
    </div>
    <table width="100%" cellpadding="0" cellspacing="0" style="border-collapse:collapse;">
      <thead>
        <tr style="background:#4C8FC0;color:white;">
          <th style="padding:5px 8px;text-align:center;font-size:11px;border:1px solid #2A6090;">QUANTITY<br>ORDERED</th>
          <th style="padding:5px 8px;text-align:center;font-size:11px;border:1px solid #2A6090;">PACK SIZE</th>
          <th style="padding:5px 8px;text-align:center;font-size:11px;border:1px solid #2A6090;">UOP</th>
          <th style="padding:5px 8px;font-size:11px;border:1px solid #2A6090;">REF ITEM</th>
          <th style="padding:5px 10px;font-size:11px;border:1px solid #2A6090;">DESCRIPTION</th>
          <th style="padding:5px 10px;text-align:right;font-size:11px;border:1px solid #2A6090;white-space:nowrap;">TOTAL VENDOR<br>EXT. COST</th>
          <th style="padding:5px 10px;text-align:right;font-size:11px;border:1px solid #2A6090;white-space:nowrap;">TOTAL NET<br>EXT. COST</th>
        </tr>
      </thead>
      <tbody>${summaryHtml}</tbody>
      <tfoot>
        <tr style="background:#D4E8F0;">
          <td colspan="5" style="padding:6px 10px;font-weight:700;font-size:12px;border:1px solid #2A6090;">GRAND TOTAL — ORDER CURRENCY: MXN</td>
          <td style="padding:6px 10px;text-align:right;font-weight:900;font-size:13px;border:1px solid #2A6090;color:#003366;">${po.total}</td>
          <td style="padding:6px 10px;text-align:right;font-weight:900;font-size:13px;border:1px solid #2A6090;color:#003366;">${po.total}</td>
        </tr>
      </tfoot>
    </table>
    <div style="padding:12px 16px;font-size:10.5px;color:#333;border-top:1px solid #ccc;line-height:1.7;">
      THIS ORDER IS PLACED BY BUYER SUBJECT TO THE TERMS AND CONDITIONS APPEARING HEREON AND ON THE ATTACHED PAGE, AND BY ACCEPTING THIS ORDER SELLER AGREES TO BE BOUND THEREBY. NO ADDITIONS OR MODIFICATIONS WILL BE BINDING UPON BUYER UNLESS EXPRESSLY AGREED TO IN WRITING.<br><br>
      1. EACH LOCATION RECEIVING MERCHANDISE MUST BE INVOICED SEPARATELY.<br>
      2. ORIGINAL INVOICE TO THE OFFICE LISTED ABOVE.<br>
      3. COPY OF INVOICE, OR PRICED PACKING SLIP, MUST ACCOMPANY THE SHIPMENT TO THE STORE.<br>
      4. OUR P.O. NUMBERS MUST APPEAR ON ALL DOCUMENTS PERTAINING TO THIS ORDER.<br>
      5. NO BACK ORDERS OR SUBSTITUTIONS WITHOUT AUTHORIZATION.
    </div>
  </div>

  <!-- ── PAGE 5: Signature ── -->
  <div style="border:1px solid #bbb;background:white;">
    <div style="display:flex;align-items:center;justify-content:space-between;padding:6px 14px;border-bottom:1px solid #ccc;background:#FAFAFA;">
      <div style="font-size:16px;font-weight:900;"><span style="color:#CC0000;">ORACLE</span><span style="color:#336699;font-weight:400;"> Retail</span></div>
      <div style="text-align:center;flex:1;"><div style="font-size:13px;font-weight:700;">Purchase Order Report</div><div style="font-size:11px;">Order No: ${po.orderNo} — FEMSA Comercio</div></div>
      <div style="font-size:10.5px;color:#555;text-align:right;">Report Date: 14-Apr-26<br>Page: 5 OF 5</div>
    </div>
    <div style="padding:40px 80px;text-align:center;">
      <div style="border-bottom:1px solid #333;width:260px;margin:0 auto 8px;"></div>
      <div style="font-size:11px;font-weight:700;letter-spacing:1px;">AUTHORIZED SIGNATURE</div>
      <div style="margin-top:30px;font-size:12px;font-weight:700;color:#333;">End of Report</div>
    </div>
  </div>

</div>`;

  const body=document.getElementById('po-modal-body');
  if(body) body.innerHTML=poHtml;
  openModal('modal-po');
}


function openOracleExcel(){
  const overlay=document.getElementById('pdf-viewer-overlay');
  const body=document.getElementById('pdf-viewer-body');
  const title=document.getElementById('pdf-viewer-title');
  if(!overlay||!body||!title) return;

  const rows=[
    {po:'76933176',site:'15AGU-216510',dest:'Aguascalientes',file:'76933176_FA216510_04142026_SERVICIOS_ADMINISTRATIVOS_15AGU-.pdf',notAfter:'22-Apr-26',skus:21,total:143544.11},
    {po:'76933072',site:'15TQV-30481',dest:'Querétaro',file:'76933072_FA30481_04142026_SERVICIOS_ADMINISTRATIVOS_15TQV.pdf',notAfter:'20-Apr-26',skus:21,total:348257.85},
    {po:'76933173',site:'15VCZ-45858',dest:'Veracruz',file:'76933173_FA45858_04142026_SERVICIOS_ADMINISTRATIVOS_15VCZ.pdf',notAfter:'21-Apr-26',skus:21,total:300534.58},
    {po:'76933065',site:'15OBQ-11309',dest:'Cd. Obregón',file:'76933065_FA11309_04142026_SERVICIOS_ADMINISTRATIVOS_15OBQ.pdf',notAfter:'21-Apr-26',skus:21,total:533410.72},
    {po:'76933070',site:'15VHD-20557',dest:'Villahermosa',file:'76933070_FA20557_04142026_SERVICIOS_ADMINISTRATIVOS_15VHD-.pdf',notAfter:'22-Apr-26',skus:20,total:464327.87},
    {po:'76933175',site:'15GUA-69098',dest:'Tlajomulco/GDL',file:'76933175_FA69098_04142026_SERVICIOS_ADMINISTRATIVOS_15GUA.pdf',notAfter:'21-Apr-26',skus:21,total:581443.84},
  ];
  const grandTotal=rows.reduce((s,r)=>s+r.total,0);
  const fmt=n=>n.toLocaleString('es-MX',{minimumFractionDigits:2});

  title.textContent='RESUMEN_OC_SERVICIOS_ADIMINISTRATIVOS_2026.xlsx';

  body.innerHTML=`
<div style="font-family:Arial,sans-serif;font-size:12px;background:white;padding:20px;">

  <!-- Excel header bar -->
  <div style="background:#217346;color:white;padding:10px 16px;display:flex;align-items:center;gap:10px;border-radius:4px 4px 0 0;margin:-20px -20px 0 -20px;">
    <svg width="20" height="20" viewBox="0 0 24 24" fill="white"><rect x="2" y="2" width="20" height="20" rx="2" fill="#1D6038"/><text x="12" y="17" text-anchor="middle" font-size="12" font-weight="900" fill="white">X</text></svg>
    <span style="font-size:13px;font-weight:700;">RESUMEN_OC_SERVICIOS_ADIMINISTRATIVOS_2026.xlsx — Microsoft Excel</span>
  </div>

  <!-- Sheet tab -->
  <div style="background:#D8E8D4;border-bottom:2px solid #217346;padding:4px 0;margin:0 -20px;">
    <span style="background:white;border:1px solid #217346;border-bottom:none;padding:4px 14px;font-size:11.5px;font-weight:700;margin-left:8px;cursor:default;">Resumen OC Sem-16</span>
    <span style="padding:4px 14px;font-size:11.5px;color:#555;cursor:default;">Detalle SKU</span>
    <span style="padding:4px 14px;font-size:11.5px;color:#555;cursor:default;">Histórico</span>
  </div>

  <!-- Title block -->
  <div style="margin:16px 0 12px 0;">
    <div style="font-size:15px;font-weight:700;color:#1D6038;">RESUMEN EJECUTIVO — ÓRDENES DE COMPRA FEMSA COMERCIO</div>
    <div style="font-size:11.5px;color:#555;">VENDOR: 101041 — SERVICIOS ADMINISTRATIVOS | Report: (ORD_DET) Oracle Retail | Semana 16 / 2026</div>
    <div style="font-size:11.5px;color:#555;">Generado: 14-Apr-26 | CONTACT: PRECIADO NORA | TEL: 6622890740</div>
  </div>

  <!-- KPI row -->
  <div style="display:flex;gap:12px;margin-bottom:16px;">
    <div style="flex:1;background:#E8F4EE;border:1px solid #217346;border-radius:4px;padding:10px;text-align:center;">
      <div style="font-size:11px;color:#555;font-weight:700;">TOTAL 6 OCs</div>
      <div style="font-size:18px;font-weight:900;color:#1D6038;">$${fmt(grandTotal)}</div>
      <div style="font-size:10px;color:#777;">MXN</div>
    </div>
    <div style="flex:1;background:#FFF8E8;border:1px solid #C8940A;border-radius:4px;padding:10px;text-align:center;">
      <div style="font-size:11px;color:#555;font-weight:700;">OC MÁS ALTA</div>
      <div style="font-size:16px;font-weight:900;color:#B8740A;">$581,443.84</div>
      <div style="font-size:10px;color:#777;">Tlajomulco / GDL</div>
    </div>
    <div style="flex:1;background:#E8EEF8;border:1px solid #336699;border-radius:4px;padding:10px;text-align:center;">
      <div style="font-size:11px;color:#555;font-weight:700;">OC MÁS URGENTE</div>
      <div style="font-size:16px;font-weight:900;color:#336699;">20-Apr-26</div>
      <div style="font-size:10px;color:#777;">Querétaro (76933072)</div>
    </div>
    <div style="flex:1;background:#F8E8E8;border:1px solid #990000;border-radius:4px;padding:10px;text-align:center;">
      <div style="font-size:11px;color:#555;font-weight:700;">SKUs PROMEDIO</div>
      <div style="font-size:18px;font-weight:900;color:#880000;">21</div>
      <div style="font-size:10px;color:#777;">por OC</div>
    </div>
  </div>

  <!-- Main table -->
  <table width="100%" cellpadding="0" cellspacing="0" style="border-collapse:collapse;">
    <thead>
      <tr style="background:#217346;color:white;">
        <th style="padding:7px 10px;text-align:center;font-size:11.5px;border:1px solid #1A5C38;">#</th>
        <th style="padding:7px 10px;font-size:11.5px;border:1px solid #1A5C38;">No. Orden</th>
        <th style="padding:7px 10px;font-size:11.5px;border:1px solid #1A5C38;">Vendor Site</th>
        <th style="padding:7px 10px;font-size:11.5px;border:1px solid #1A5C38;">Destino</th>
        <th style="padding:7px 10px;font-size:11.5px;border:1px solid #1A5C38;">Archivo PDF</th>
        <th style="padding:7px 10px;text-align:center;font-size:11.5px;border:1px solid #1A5C38;white-space:nowrap;">Not After</th>
        <th style="padding:7px 10px;text-align:center;font-size:11.5px;border:1px solid #1A5C38;">SKUs</th>
        <th style="padding:7px 10px;text-align:right;font-size:11.5px;border:1px solid #1A5C38;white-space:nowrap;">Total MXN</th>
        <th style="padding:7px 10px;text-align:center;font-size:11.5px;border:1px solid #1A5C38;">Estado</th>
      </tr>
    </thead>
    <tbody>
      ${rows.map((r,i)=>`
      <tr style="background:${i%2===0?'white':'#F4FAF6'};">
        <td style="border:1px solid #C8DCC8;padding:6px 10px;text-align:center;font-size:11.5px;color:#777;">${i+1}</td>
        <td style="border:1px solid #C8DCC8;padding:6px 10px;font-size:12px;font-weight:700;color:#1D6038;">${r.po}</td>
        <td style="border:1px solid #C8DCC8;padding:6px 10px;font-size:11px;color:#555;">${r.site}</td>
        <td style="border:1px solid #C8DCC8;padding:6px 10px;font-size:12px;font-weight:700;">${r.dest}</td>
        <td style="border:1px solid #C8DCC8;padding:6px 10px;font-size:10px;color:#336699;">${r.file}</td>
        <td style="border:1px solid #C8DCC8;padding:6px 10px;text-align:center;font-size:11.5px;${r.notAfter==='20-Apr-26'?'color:#CC0000;font-weight:700;':''}">${r.notAfter}</td>
        <td style="border:1px solid #C8DCC8;padding:6px 10px;text-align:center;font-size:11.5px;">${r.skus}</td>
        <td style="border:1px solid #C8DCC8;padding:6px 10px;text-align:right;font-size:12px;font-weight:700;">$${fmt(r.total)}</td>
        <td style="border:1px solid #C8DCC8;padding:6px 10px;text-align:center;">
          <span style="background:#FFF3CD;color:#856404;border:1px solid #FFC107;border-radius:10px;padding:2px 8px;font-size:10.5px;font-weight:700;">Pendiente</span>
        </td>
      </tr>`).join('')}
    </tbody>
    <tfoot>
      <tr style="background:#C8E6C9;">
        <td colspan="7" style="border:1px solid #1A5C38;padding:7px 10px;font-size:12px;font-weight:900;">TOTAL GENERAL — 6 ÓRDENES DE COMPRA</td>
        <td style="border:1px solid #1A5C38;padding:7px 10px;text-align:right;font-size:14px;font-weight:900;color:#1D6038;">$${fmt(grandTotal)}</td>
        <td style="border:1px solid #1A5C38;"></td>
      </tr>
    </tfoot>
  </table>

  <div style="margin-top:14px;font-size:10.5px;color:#777;">
    Reporte generado automáticamente por el sistema Oracle Retail (ORD_DET) FEMSA Comercio | 14-Abr-2026<br>
    Todos los precios en MXN. Términos: 30 días. Descuento: 0.00%. Carga Masiva RMS.
  </div>
</div>`;

  overlay.style.display='flex';
  showToast('📊 Abriendo Excel — Resumen OC Servicios Administrativos 2026');
}


function openPOViewerFromEmail(emailId, fileName){
  const email = emailsData.find(e=>e.id===emailId);
  if(!email){ showToast('Email no encontrado'); return; }
  const attach = email.attachments ? email.attachments.find(a=>a.name===fileName) : null;

  // ── Excel resumen ────────────────────────────────────────────
  if(fileName.endsWith('.xlsx')){
    showOracleModal('RESUMEN OC \u2014 SERVICIOS ADMINISTRATIVOS 2026', renderExcelSummary());
    return;
  }

  // ── Real Oracle Retail PDF ────────────────────────────────────
  if(attach && attach.poId && REAL_POS[attach.poId]){
    const po = REAL_POS[attach.poId];
    showOracleModal('OC '+po.orderNo+' \u2014 '+po.shipTo+' \u2014 Oracle Retail (ORD_DET)', renderOraclePO(attach.poId));
    return;
  }

  // ── Legacy fallback ───────────────────────────────────────────
  const rd = (typeof repoDocs !== 'undefined') ? repoDocs.find(d=>d.emailId===emailId && d.name===fileName) : null;
  if(rd){ openDocumentPDF(rd.id); return; }
  showToast('\ud83d\udcc4 Abriendo: '+fileName);
}

function showOracleModal(title, htmlContent){
  const ex = document.getElementById('oracle-po-modal');
  if(ex) ex.remove();
  const modal = document.createElement('div');
  modal.id='oracle-po-modal';
  modal.style.cssText='position:fixed;inset:0;background:rgba(0,0,0,.55);z-index:9999;display:flex;align-items:flex-start;justify-content:center;padding-top:40px;overflow-y:auto;';
  modal.innerHTML=`
    <div style="background:white;width:96%;max-width:960px;border-radius:6px;box-shadow:0 8px 40px rgba(0,0,0,.3);overflow:hidden;margin-bottom:40px;">
      <div style="display:flex;align-items:center;justify-content:space-between;padding:10px 16px;background:#2A5DAB;color:white;">
        <div style="display:flex;align-items:center;gap:8px;">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="white"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg>
          <span style="font-family:Arial;font-size:13px;font-weight:700;">${title}</span>
        </div>
        <button onclick="document.getElementById('oracle-po-modal').remove()" style="background:rgba(255,255,255,.2);border:none;color:white;width:26px;height:26px;border-radius:50%;cursor:pointer;font-size:16px;display:flex;align-items:center;justify-content:center;">&#x2715;</button>
      </div>
      <div style="overflow-y:auto;max-height:80vh;padding:16px;">${htmlContent}</div>
    </div>`;
  document.body.appendChild(modal);
  modal.addEventListener('click', e=>{ if(e.target===modal) modal.remove(); });
}


function renderReportes(){
  const tot=DATASET.all.length;
  const suc=DATASET.success.length;
  const err=DATASET.errors.length;
  const blg=DATASET.backlog.length;
  const autoRate=Math.round((suc/tot)*100);
  const errRate=((err/tot)*100).toFixed(1);
  const avgPT=(DATASET.success.reduce((s,o)=>s+(o.processingTime||0),0)/Math.max(suc,1)).toFixed(1);
  const totalMXN=DATASET.success.reduce((s,o)=>s+o.totalMXN,0);

  // ── KPI Cards ──
  const kpis=[
    {label:'Total OCs Recibidas — 10 días',val:tot.toLocaleString('es-MX'),sub:`~${Math.round(tot/10)} OC/día · proyección: ~4,100/mes`,cls:'blue'},
    {label:'Procesadas en SAP SD',val:suc.toLocaleString('es-MX'),sub:`${autoRate}% tasa de automatización · target ≥ 85%`,cls:'green'},
    {label:'Valor Total Procesado',val:'$'+Math.round(totalMXN/1000).toLocaleString('es-MX')+'K MXN',sub:`Promedio $${Math.round(totalMXN/suc).toLocaleString('es-MX')} por pedido`,cls:'orange'},
    {label:'Errores Detectados',val:err.toLocaleString('es-MX'),sub:`${errRate}% tasa de error · target ≤ 2%`,cls:parseFloat(errRate)<=2?'green':'red'},
  ];
  const kpiEl=document.getElementById('rpt-kpis');
  if(kpiEl) kpiEl.innerHTML=kpis.map(k=>`<div class="rpt-kpi ${k.cls}"><div class="rpt-kpi-label">${k.label}</div><div class="rpt-kpi-val">${k.val}</div><div class="rpt-kpi-sub">${k.sub}</div></div>`).join('');

  // ── Stacked bar chart — 10 days ──
  const maxVol=Math.max(...DAY_STATS.map(d=>d.total),1);
  const chartEl=document.getElementById('rpt-bar-chart');
  if(chartEl) chartEl.innerHTML=DAY_STATS.map(ds=>{
    const isFest=ds.vol<60;
    const pctS=Math.round((ds.success/Math.max(ds.total,1))*100);
    const pctB=Math.round((ds.backlog/Math.max(ds.total,1))*100);
    const pctE=Math.round((ds.errors/Math.max(ds.total,1))*100);
    const barH=Math.max(4,Math.round((ds.total/maxVol)*140));
    return `<div style="flex:1;display:flex;flex-direction:column;align-items:center;cursor:pointer;padding:0 3px;" onclick="setLCDate('${ds.date}');navigate('lifecycle')" title="${ds.dow}: ${ds.total} pedidos">
      <div style="font-size:10px;font-weight:700;color:var(--sub);margin-bottom:4px;">${ds.total}</div>
      <div style="width:100%;height:${barH}px;border-radius:4px 4px 0 0;overflow:hidden;display:flex;flex-direction:column-reverse;">
        <div style="width:100%;height:${pctS}%;background:var(--green);min-height:${ds.success>0?2:0}px;"></div>
        <div style="width:100%;height:${pctB}%;background:var(--amber);min-height:${ds.backlog>0?2:0}px;"></div>
        <div style="width:100%;height:${pctE}%;background:var(--red);min-height:${ds.errors>0?2:0}px;"></div>
      </div>
      <div style="font-size:9.5px;font-weight:700;color:${isFest?'var(--red-tx)':'var(--sub)'};text-align:center;margin-top:6px;line-height:1.3;">${ds.label.replace(' ','\n')}</div>
      ${isFest?'<div style="font-size:8.5px;color:var(--red-tx);">festivo</div>':''}
    </div>`;
  }).join('');

  // ── Top Areas ──
  const areaMap={};
  DATASET.all.forEach(o=>{if(!areaMap[o.areaShort]) areaMap[o.areaShort]={n:0,rev:0};areaMap[o.areaShort].n++;areaMap[o.areaShort].rev+=o.status==='success'?o.totalMXN:0;});
  const sortedAreas=Object.entries(areaMap).sort((a,b)=>b[1].n-a[1].n).slice(0,10);
  const maxA=sortedAreas[0]?sortedAreas[0][1].n:1;
  const areasEl=document.getElementById('rpt-top-areas');
  if(areasEl) areasEl.innerHTML=sortedAreas.map(([name,d],i)=>`<div class="rpt-bar-row">
    <div style="font-size:11px;font-weight:600;min-width:20px;color:var(--sub);">${i+1}</div>
    <div class="rpt-bar-label">${name}</div>
    <div class="rpt-bar-track"><div class="rpt-bar-fill" style="width:${Math.round(d.n/maxA*100)}%;background:var(--orange);"></div></div>
    <div class="rpt-bar-val" style="min-width:65px;">${d.n} <span style="font-size:10px;color:var(--sub);">pedidos</span></div>
  </div>`).join('');

  // ── Error Types ──
  const errMap={};
  DATASET.errors.forEach(o=>{errMap[o.errorCode]=(errMap[o.errorCode]||0)+1;});
  const sortedErrs=Object.entries(errMap).sort((a,b)=>b[1]-a[1]);
  const errEl=document.getElementById('rpt-err-types');
  if(errEl) errEl.innerHTML=sortedErrs.map(([code,n])=>{
    const sample=DATASET.errors.find(o=>o.errorCode===code);
    const pct=((n/err)*100).toFixed(0);
    return `<div class="rpt-err-type">
      <div>
        <div class="rpt-err-badge">${code}</div>
        <div style="font-size:11px;color:var(--sub);margin-top:3px;">${sample?sample.errorTitle:code}</div>
      </div>
      <div style="text-align:right;">
        <div style="font-size:16px;font-weight:800;color:var(--red-tx);">${n}</div>
        <div style="font-size:10px;color:var(--sub);">${pct}% del total</div>
      </div>
    </div>`;
  }).join('');

  // ── City Distribution ──
  const cityMap={};
  DATASET.all.forEach(o=>{cityMap[o.storeCity]=(cityMap[o.storeCity]||0)+1;});
  const sortedCities=Object.entries(cityMap).sort((a,b)=>b[1]-a[1]);
  const maxC=sortedCities[0]?sortedCities[0][1]:1;
  const cityEl=document.getElementById('rpt-city-dist');
  if(cityEl) cityEl.innerHTML=sortedCities.map(([city,n])=>`<div class="rpt-bar-row">
    <div class="rpt-bar-label">${city}</div>
    <div class="rpt-bar-track"><div class="rpt-bar-fill" style="width:${Math.round(n/maxC*100)}%;background:#3B82F6;"></div></div>
    <div class="rpt-bar-val">${n}</div>
  </div>`).join('');

  // ── Processing Time Trend ──
  const trendEl=document.getElementById('rpt-pt-trend');
  if(trendEl) trendEl.innerHTML=DAY_STATS.map(ds=>{
    const dayOrds=DATASET.success.filter(o=>o.date===ds.date);
    const avg=dayOrds.length>0?(dayOrds.reduce((s,o)=>s+(o.processingTime||0),0)/dayOrds.length).toFixed(1):'—';
    const col=avg==='—'?'var(--sub)':parseFloat(avg)<=3?'var(--green)':parseFloat(avg)<=5?'var(--amber)':'var(--red)';
    const isFest=ds.vol<60;
    return `<div style="display:flex;align-items:center;gap:12px;padding:7px 0;border-bottom:1px solid var(--border);">
      <div class="rpt-trend-dot" style="background:${col};"></div>
      <div style="flex:1;font-size:12.5px;color:${isFest?'var(--sub)':'var(--text)'};">${ds.label}${isFest?' <span style="font-size:10px;color:var(--red-tx);">(festivo)</span>':''}</div>
      <div style="font-weight:800;font-size:14px;color:${col};min-width:55px;text-align:right;">${avg} min</div>
      <div style="font-size:10.5px;color:var(--sub);min-width:80px;text-align:right;">${dayOrds.length.toLocaleString()} procesados</div>
    </div>`;
  }).join('');

  // ── SKU Ranking ──
  const skuMap={};
  DATASET.all.forEach(o=>o.items.forEach(it=>{
    if(!skuMap[it.sku]) skuMap[it.sku]={sku:it.sku,desc:it.desc,qty:0,orders:0,rev:0};
    skuMap[it.sku].qty+=it.qty;
    skuMap[it.sku].orders++;
    skuMap[it.sku].rev+=it.importe;
  }));
  const sortedSkus=Object.values(skuMap).sort((a,b)=>b.orders-a.orders).slice(0,10);
  const maxSku=sortedSkus[0]?sortedSkus[0].orders:1;
  const skuEl=document.getElementById('rpt-sku-rank');
  if(skuEl) skuEl.innerHTML=sortedSkus.map((s,i)=>`<div class="rpt-bar-row">
    <div style="font-size:11px;font-weight:600;min-width:20px;color:var(--sub);">${i+1}</div>
    <div class="rpt-bar-label" style="min-width:100px;font-family:var(--mono);font-size:10.5px;color:var(--blue-tx);">${s.sku}</div>
    <div class="rpt-bar-track"><div class="rpt-bar-fill" style="width:${Math.round(s.orders/maxSku*100)}%;background:var(--teal);"></div></div>
    <div style="font-size:11px;color:var(--sub);min-width:90px;text-align:right;">${s.orders.toLocaleString()} líneas</div>
  </div>`).join('');

  // ── SLA Summary Table ──
  const slaEl=document.getElementById('rpt-sla-table');
  if(slaEl){
    const rows=[
      {sla:'SLA 1 — Ingesta (≤ 5 min)',val:avgPT+' min avg',pct:'100%',target:'≤ 5 min',ok:parseFloat(avgPT)<=5},
      {sla:'SLA 2 — Automatización (≥ 85%)',val:autoRate+'%',pct:autoRate+'%',target:'≥ 85%',ok:autoRate>=85},
      {sla:'Tasa de Error (≤ 2%)',val:errRate+'%',pct:errRate+'%',target:'≤ 2%',ok:parseFloat(errRate)<=2},
      {sla:'OTD — On-Time Delivery',val:'En evaluación',pct:'94%',target:'≥ 95%',ok:false},
      {sla:'% Notas de Crédito',val:'3.2%',pct:'3.2%',target:'≤ 2%',ok:false},
    ];
    slaEl.innerHTML=`<table style="width:100%;border-collapse:collapse;font-size:13px;">
      <thead><tr style="background:var(--light);">
        <th style="text-align:left;padding:10px 14px;font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;border-bottom:2px solid var(--border);">Indicador SLA</th>
        <th style="text-align:center;padding:10px 14px;font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;border-bottom:2px solid var(--border);">Target</th>
        <th style="text-align:center;padding:10px 14px;font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;border-bottom:2px solid var(--border);">Resultado 10 días</th>
        <th style="text-align:center;padding:10px 14px;font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;border-bottom:2px solid var(--border);">Estado</th>
        <th style="text-align:center;padding:10px 14px;font-size:10px;font-weight:700;color:var(--sub);letter-spacing:.8px;text-transform:uppercase;border-bottom:2px solid var(--border);">Tendencia</th>
      </tr></thead>
      <tbody>${rows.map(r=>`<tr style="border-bottom:1px solid var(--border);" onmouseover="this.style.background='var(--light)'" onmouseout="this.style.background=''">
        <td style="padding:12px 14px;font-weight:600;">${r.sla}</td>
        <td style="padding:12px 14px;text-align:center;font-family:var(--mono);color:var(--sub);">${r.target}</td>
        <td style="padding:12px 14px;text-align:center;font-weight:800;font-size:15px;color:${r.ok?'var(--green-tx)':'var(--red-tx)'};">${r.val}</td>
        <td style="padding:12px 14px;text-align:center;"><span style="display:inline-flex;align-items:center;gap:5px;padding:4px 12px;border-radius:20px;font-size:11px;font-weight:700;background:${r.ok?'var(--green-bg)':'var(--red-bg)'};color:${r.ok?'var(--green-tx)':'var(--red-tx)'};">${r.ok?'✅ CUMPLIDO':'❌ POR MEJORAR'}</span></td>
        <td style="padding:12px 14px;text-align:center;font-size:18px;">${r.ok?'📈':'📉'}</td>
      </tr>`).join('')}</tbody>
    </table>`;
  }
}

// ════════════════════════════════════════════
function renderControlTower(){
  const tot=DATASET.all.length;
  const suc=DATASET.success.length;
  const err=DATASET.errors.length;
  const blg=DATASET.backlog.length;
  const autoRate=Math.round((suc/tot)*100);
  const errRate=((err/tot)*100).toFixed(1);
  const avgPT=(DATASET.success.reduce((s,o)=>s+(o.processingTime||0),0)/Math.max(suc,1)).toFixed(1);
  const totalMXN=DATASET.success.reduce((s,o)=>s+o.totalMXN,0);
  const TODAY_ISO='2026-05-04';

  // ── CHART 1: Volúmenes Procesados por día (Image 3 style) ──────────────────
  const maxProc=Math.max(...DAY_STATS.map(d=>d.success),1);
  const procEl=document.getElementById('ct-proc-chart');
  const procLblEl=document.getElementById('ct-proc-labels');
  const procStatsEl=document.getElementById('ct-proc-stats');
  if(procEl){
    procEl.innerHTML=DAY_STATS.map((ds,i)=>{
      const h=Math.max(4,Math.round((ds.success/maxProc)*128));
      const isFest=ds.total<60;
      const barColor=isFest?'rgba(107,114,128,.5)':ds.success>=100?'rgba(34,197,94,.9)':ds.success>=50?'rgba(249,115,22,.8)':'rgba(249,115,22,.5)';
      return `<div style="flex:1;display:flex;flex-direction:column;align-items:center;cursor:pointer;min-width:0;" onclick="setLCDate('${ds.date}');navigate('lifecycle')" title="${ds.dow}: ${ds.success} procesados">
        <div style="font-size:9.5px;font-weight:800;color:rgba(255,255,255,.75);margin-bottom:3px;">${ds.success}</div>
        <div style="width:90%;height:${h}px;border-radius:4px 4px 0 0;background:${barColor};position:relative;overflow:hidden;">
          ${ds.backlog>0?`<div style="position:absolute;bottom:0;width:100%;height:${Math.round((ds.backlog/(ds.total||1))*h)}px;background:rgba(245,158,11,.6);"></div>`:''}
        </div>
      </div>`;
    }).join('');
  }
  if(procLblEl){
    procLblEl.innerHTML=DAY_STATS.map(ds=>`<div style="flex:1;text-align:center;font-size:8px;color:rgba(255,255,255,.4);padding-top:4px;line-height:1.4;min-width:0;">${ds.label.split(' ').join('<br>')}</div>`).join('');
  }
  if(procStatsEl){
    const pico=DAY_STATS.reduce((m,d)=>d.success>m.success?d:m,DAY_STATS[0]);
    procStatsEl.innerHTML=
      `<div style="background:rgba(255,255,255,.07);border-radius:10px;padding:10px 14px;text-align:center;min-width:90px;"><div style="font-size:9px;color:rgba(255,255,255,.4);text-transform:uppercase;letter-spacing:.8px;margin-bottom:3px;">Total 10 días</div><div style="font-size:20px;font-weight:800;color:white;">${suc.toLocaleString()}</div></div>`+
      `<div style="background:rgba(255,255,255,.07);border-radius:10px;padding:10px 14px;text-align:center;min-width:90px;"><div style="font-size:9px;color:rgba(255,255,255,.4);text-transform:uppercase;letter-spacing:.8px;margin-bottom:3px;">Promedio/día</div><div style="font-size:20px;font-weight:800;color:white;">${Math.round(suc/10)}</div></div>`+
      `<div style="background:rgba(255,255,255,.07);border-radius:10px;padding:10px 14px;text-align:center;min-width:90px;"><div style="font-size:9px;color:rgba(255,255,255,.4);text-transform:uppercase;letter-spacing:.8px;margin-bottom:3px;">Pico (${pico.label})</div><div style="font-size:20px;font-weight:800;color:#4ADE80;">${pico.success}</div></div>`;
  }

  // ── CHART 2: Aging de Pendientes + Errores ─────────────────────────────────
  const agingEl=document.getElementById('ct-aging-chart');
  const agingStEl=document.getElementById('ct-aging-stats');
  if(agingEl){
    const today=new Date('2026-05-04');
    const pending=[...backlogData,...errorsData];
    const buckets={'Hoy (0d)':{n:0,col:'#4ADE80'},'1–2 días':{n:0,col:'#FCD34D'},'3–5 días':{n:0,col:'#FB923C'},'6+ días':{n:0,col:'#F87171'}};
    pending.forEach(o=>{
      const parts=o.date.split('/');
      const arrived=new Date(`${parts[2]}-${parts[1]}-${parts[0]}`);
      const days=Math.floor((today-arrived)/(1000*60*60*24));
      if(days===0) buckets['Hoy (0d)'].n++;
      else if(days<=2) buckets['1–2 días'].n++;
      else if(days<=5) buckets['3–5 días'].n++;
      else buckets['6+ días'].n++;
    });
    const maxBuck=Math.max(...Object.values(buckets).map(b=>b.n),1);
    agingEl.innerHTML='<div style="display:flex;flex-direction:column;gap:10px;">'+
      Object.entries(buckets).map(([k,v])=>`
        <div>
          <div style="display:flex;justify-content:space-between;margin-bottom:5px;">
            <span style="font-size:12px;font-weight:600;color:rgba(255,255,255,.75);">${k}</span>
            <span style="font-size:13px;font-weight:800;color:${v.col};">${v.n} pedidos</span>
          </div>
          <div style="height:8px;background:rgba(255,255,255,.1);border-radius:4px;overflow:hidden;">
            <div style="height:100%;width:${Math.round(v.n/maxBuck*100)}%;background:${v.col};border-radius:4px;transition:width .8s;"></div>
          </div>
        </div>`).join('')+
      '</div>';
    if(agingStEl){
      const avgDays=pending.length>0?(pending.reduce((s,o)=>{
        const parts=o.date.split('/');const arrived=new Date(`${parts[2]}-${parts[1]}-${parts[0]}`);
        return s+Math.floor((today-arrived)/(1000*60*60*24));
      },0)/pending.length).toFixed(1):'0';
      agingStEl.innerHTML=
        `<div style="background:rgba(255,255,255,.07);border-radius:10px;padding:10px;text-align:center;"><div style="font-size:9px;color:rgba(255,255,255,.4);text-transform:uppercase;letter-spacing:.8px;margin-bottom:2px;">Total Pendientes</div><div style="font-size:20px;font-weight:800;color:#FCD34D;">${pending.length.toLocaleString()}</div></div>`+
        `<div style="background:rgba(255,255,255,.07);border-radius:10px;padding:10px;text-align:center;"><div style="font-size:9px;color:rgba(255,255,255,.4);text-transform:uppercase;letter-spacing:.8px;margin-bottom:2px;">Edad Promedio</div><div style="font-size:20px;font-weight:800;color:#F87171;">${avgDays} días</div></div>`;
    }
  }

  // ── CHART 3: Por Tipo de Cliente ────────────────────────────────────────────
  const clientEl=document.getElementById('ct-client-chart');
  if(clientEl){
    const areaMap={};
    DATASET.all.forEach(o=>{
      if(!areaMap[o.areaShort]) areaMap[o.areaShort]={name:o.areaShort,total:0,ok:0,pend:0,err:0};
      areaMap[o.areaShort].total++;
      if(o.status==='success') areaMap[o.areaShort].ok++;
      else if(o.status==='backlog') areaMap[o.areaShort].pend++;
      else areaMap[o.areaShort].err++;
    });
    const sorted=Object.values(areaMap).sort((a,b)=>b.total-a.total).slice(0,8);
    const maxA=sorted[0]?sorted[0].total:1;
    clientEl.innerHTML='<div style="display:flex;flex-direction:column;gap:8px;">'+
      sorted.map(a=>`
        <div>
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:4px;">
            <span style="font-size:11.5px;font-weight:600;color:rgba(255,255,255,.8);">${a.name}</span>
            <span style="font-size:11.5px;font-weight:700;color:rgba(255,255,255,.7);">${a.total}</span>
          </div>
          <div style="height:10px;background:rgba(255,255,255,.1);border-radius:5px;overflow:hidden;display:flex;">
            <div style="height:100%;width:${Math.round(a.ok/maxA*100)}%;background:#22C55E;"></div>
            <div style="height:100%;width:${Math.round(a.pend/maxA*100)}%;background:#F59E0B;"></div>
            <div style="height:100%;width:${Math.round(a.err/maxA*100)}%;background:#EF4444;"></div>
          </div>
        </div>`).join('')+
      '</div>'+
      '<div style="display:flex;gap:14px;margin-top:12px;">'+
      [['#22C55E','Procesados'],['#F59E0B','Backlog'],['#EF4444','Errores']].map(([c,l])=>
        `<div style="display:flex;align-items:center;gap:5px;font-size:10.5px;color:rgba(255,255,255,.5);">
          <div style="width:10px;height:10px;border-radius:2px;background:${c};"></div>${l}</div>`).join('')+
      '</div>';
  }

  // ── CHART 4: Top Materiales + Stock ─────────────────────────────────────────
  const matsEl=document.getElementById('ct-materials-chart');
  if(matsEl){
    // Count orders per SKU
    const skuMap={};
    DATASET.all.forEach(o=>o.items.forEach(it=>{
      if(!skuMap[it.sku]) skuMap[it.sku]={sku:it.sku,desc:it.desc,orders:0,qty:0};
      skuMap[it.sku].orders++;
      skuMap[it.sku].qty+=it.qty;
    }));
    // Simulated stock (proportional to demand, some in shortage)
    const SEED_STOCK={'CAF-001-1KG':320,'CAF-MOL-500G':480,'CAF-ESP-250G':210,'LEC-001-1L':950,'LEC-DES-1L':420,'LAL-001-946':180,'LAV-001-946':150,'VAS-012-50PK':85,'PKG-602':42,'PKG-601':95,'AZU-050-KG':65,'AZU-001-KG':380,'JAR-500ML':120,'PAJ-IND-25':290,'SER-NAP-200':340};
    const sorted=Object.values(skuMap).sort((a,b)=>b.orders-a.orders).slice(0,10);
    const maxO=sorted[0]?sorted[0].orders:1;
    const maxS=Math.max(...sorted.map(s=>SEED_STOCK[s.sku]||0),1);
    const combinedMax=Math.max(maxO,maxS);
    matsEl.innerHTML='<div style="display:grid;grid-template-columns:1fr;gap:10px;">'+
      sorted.map((s,i)=>{
        const stock=SEED_STOCK[s.sku]||0;
        const stockPct=Math.round(stock/combinedMax*100);
        const orderPct=Math.round(s.orders/combinedMax*100);
        const lowStock=stock<s.orders*0.5;
        return `<div>
          <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:5px;">
            <div style="display:flex;align-items:center;gap:8px;">
              <span style="font-size:10px;font-weight:700;color:rgba(255,255,255,.3);min-width:16px;">${i+1}</span>
              <span style="font-family:var(--mono);font-size:11px;font-weight:600;color:var(--teal);">${s.sku}</span>
              <span style="font-size:10.5px;color:rgba(255,255,255,.5);">${s.desc.substring(0,28)}…</span>
              ${lowStock?'<span style="font-size:9.5px;font-weight:700;background:rgba(239,68,68,.2);color:#F87171;padding:1px 6px;border-radius:8px;">⚠ Stock bajo</span>':''}
            </div>
            <div style="display:flex;gap:14px;text-align:right;">
              <span style="font-size:11.5px;font-weight:700;color:var(--teal);">${s.orders} líneas</span>
              <span style="font-size:11.5px;font-weight:700;color:${lowStock?'#F87171':'rgba(249,115,22,.9)'};">${stock.toLocaleString()} uds</span>
            </div>
          </div>
          <div style="position:relative;height:14px;background:rgba(255,255,255,.06);border-radius:7px;overflow:hidden;">
            <div style="position:absolute;left:0;top:0;height:100%;width:${orderPct}%;background:var(--teal);border-radius:7px;opacity:.85;"></div>
            <div style="position:absolute;left:0;top:3px;height:8px;width:${stockPct}%;background:${lowStock?'#F87171':'rgba(249,115,22,.7)'};border-radius:4px;opacity:.7;"></div>
          </div>
        </div>`;
      }).join('')+
      '</div>';
  }

  // ── SLA Performance ──────────────────────────────────────────────────────────
  const slaEl=document.getElementById('ct-sla-content');
  if(slaEl){
    const aiTxt=`Análisis ${tot.toLocaleString()} OCs · ${suc.toLocaleString()} procesadas · ${autoRate}% automatización · ${avgPT} min tiempo promedio · Tasa de error: ${errRate}% · Valor procesado: $${Math.round(totalMXN/1000).toLocaleString()}K MXN`;
    const slaItems=[
      ['SLA 1 — Ingesta (OC → PV SAP)',`${avgPT} min`,100,parseFloat(avgPT)<=5,'var(--green)','target ≤ 5 min'],
      ['SLA 2 — Entrega (PV → lista)','87%',87,true,'var(--green)','target ≤ 2 hrs'],
      ['% Automatización',`${autoRate}%`,autoRate,autoRate>=85,autoRate>=85?'var(--green)':'var(--amber)','target ≥ 85%'],
      ['Tasa de Error',`${errRate}%`,Math.min(parseFloat(errRate)*20,100),parseFloat(errRate)<=2,parseFloat(errRate)<=2?'var(--green)':'var(--red)','target ≤ 2%'],
      ['OTD — On-Time Delivery','94%',94,true,'var(--green)','target ≥ 95%'],
      ['% Notas de Crédito','3.2%',16,false,'var(--amber)','target ≤ 2%'],
    ];
    slaEl.innerHTML=
      `<div style="display:grid;grid-template-columns:1fr 320px;gap:20px;">
        <div>
          <div class="ct-ai-box"><div class="ct-ai-label">🤖 AI Bottleneck Analysis</div><div class="ct-ai-text" id="ct-ai-text">${aiTxt}</div></div>
          <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:12px;">
            <div>${slaItems.slice(0,3).map(s=>`<div class="sla-row"><div class="sla-row-top"><span class="sla-row-label">${s[0]}</span><div class="sla-row-right"><span class="sla-row-pct" style="color:${s[4]};">${s[1]}</span><span class="sla-row-target">${s[5]}</span></div></div><div class="sla-track"><div class="sla-fill" style="width:${Math.min(s[2],100)}%;background:${s[4]};"></div></div></div>`).join('')}</div>
            <div>${slaItems.slice(3).map(s=>`<div class="sla-row"><div class="sla-row-top"><span class="sla-row-label">${s[0]}</span><div class="sla-row-right"><span class="sla-row-pct" style="color:${s[4]};">${s[1]}</span><span class="sla-row-target">${s[5]}</span></div></div><div class="sla-track"><div class="sla-fill" style="width:${Math.min(s[2],100)}%;background:${s[4]};"></div></div></div>`).join('')}</div>
          </div>
        </div>
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;align-content:start;">
          <div class="ct-metric"><div class="ct-metric-lbl">⏱ Avg Time</div><div class="ct-metric-val">${avgPT}m</div></div>
          <div class="ct-metric"><div class="ct-metric-lbl">🔄 Auto Rate</div><div class="ct-metric-val" style="color:#4ADE80;">${autoRate}%</div></div>
          <div class="ct-metric"><div class="ct-metric-lbl">⚠ Error Rate</div><div class="ct-metric-val" style="color:#F87171;">${errRate}%</div></div>
          <div class="ct-metric"><div class="ct-metric-lbl">📦 Total OCs</div><div class="ct-metric-val">${tot.toLocaleString()}</div></div>
          <div class="ct-metric"><div class="ct-metric-lbl">📈 OTD</div><div class="ct-metric-val" style="color:#4ADE80;">94%</div></div>
          <div class="ct-metric"><div class="ct-metric-lbl">📄 NC</div><div class="ct-metric-val" style="color:#FCD34D;">3.2%</div></div>
        </div>
      </div>`;
  }
}

function updateCT(){ renderControlTower(); showToast('📊 Dashboard actualizado'); }

function runBottleneck(){
  const el=document.getElementById('ct-ai-text');
  if(!el) return;
  el.textContent='🤖 Analizando '+DATASET.all.length.toLocaleString()+' pedidos OTC…';
  const res=[
    `${DATASET.all.length.toLocaleString()} OCs procesadas. Auto: ${Math.round(DATASET.success.length/DATASET.all.length*100)}%. Cuello de botella: festivo 01/05 (48 pedidos). Recomendación: activar auto-release clientes VIP, ampliar whitelist @oxxo.com.mx.`,
    `${DATASET.errors.length} errores en 10 días (${((DATASET.errors.length/DATASET.all.length)*100).toFixed(1)}%). Causa: SKU-404 y CUST-MAP. Fuzzy-match reducirá error rate a <2%. Tiempo promedio: ${(DATASET.success.reduce((s,o)=>s+(o.processingTime||0),0)/Math.max(DATASET.success.length,1)).toFixed(1)} min — dentro de SLA.`,
  ];
  setTimeout(()=>{if(el) el.textContent=res[Math.floor(Math.random()*res.length)];showToast('✅ Análisis completado');},1800);
}

// ── Observatory (was renderObservatory, etc.) ──
function renderObservatory(){ renderAgentList(''); selectAgent(activeObsAgent||'ag01'); }
function renderAgentList(filter){
  const filtered=agentsData.filter(a=>a.name.toLowerCase().includes(filter.toLowerCase()));
  const el=document.getElementById('obs-agent-list'); if(!el) return;
  el.innerHTML=filtered.map(a=>`<div class="obs-agent-item ${a.id===activeObsAgent?'active':''}" onclick="selectAgent('${a.id}')" id="obs-item-${a.id}"><span class="obs-agent-dot ${a.status}"></span><span class="obs-agent-name">${a.name}</span>${a.id===activeObsAgent?'<span class="obs-agent-chevron">›</span>':''}</div>`).join('');
}
function filterAgents(q){ renderAgentList(q); }
function selectAgent(id){
  activeObsAgent=id; renderAgentList(document.getElementById('obs-search')?document.getElementById('obs-search').value:'');
  const ag=agentsData.find(a=>a.id===id); if(!ag) return;
  const statusClass={'running':'obs-badge-running','idle':'obs-badge-idle','error':'obs-badge-error'}[ag.status];
  const statusLabel={'running':'RUNNING','idle':'IDLE','error':'ERROR'}[ag.status];
  const now=new Date();
  const sampleLogs=[{type:'ok',text:'Agent cycle completed successfully',offset:5},{type:'ok',text:'RFC connection to CAF1: 200ms',offset:67},{type:ag.status==='error'?'err':'ok',text:ag.status==='error'?'ERROR: Mapping failed — d70f20b4':'All validations passed — SAP 200ms',offset:132},{type:'ok',text:'Queue processed: '+Math.floor(Math.random()*5+1)+' items',offset:198},{type:Math.random()>.7?'warn':'ok',text:Math.random()>.7?'WARNING: Processing near SLA':'Heartbeat — Agent alive',offset:265}];
  const mainEl=document.getElementById('obs-main'); if(!mainEl) return;
  mainEl.innerHTML=`<div class="obs-main-header"><div class="obs-agent-title">${ag.name}</div><div class="obs-status-row"><span class="obs-running-badge ${statusClass}">${statusLabel}</span><div class="obs-stat"><div class="obs-stat-val" style="color:${ag.confidence>=90?'#2dd4bf':'#fbbf24'};">${ag.confidence}%</div><div class="obs-stat-lbl">Confidence</div></div><div class="obs-stat"><div class="obs-stat-val" style="color:${ag.impact==='High'?'#2dd4bf':'#6b7280'};">${ag.impact}</div><div class="obs-stat-lbl">Impact</div></div><div class="obs-stat"><div class="obs-stat-val">${ag.rate}%</div><div class="obs-stat-lbl">Rate</div></div></div></div><div class="obs-main-body"><div><div class="obs-card"><div class="obs-card-title"><div class="obs-card-icon" style="background:rgba(20,184,166,.15);">🎯</div><div class="obs-card-title-text">Agent Purpose &amp; ML Definition</div></div><div class="obs-card-sub">${ag.purpose}</div></div><div class="obs-card"><div class="obs-card-title"><div class="obs-card-icon" style="background:rgba(59,130,246,.15);">🗄️</div><div class="obs-card-title-text">Data Vectors</div></div>${ag.dataVectors.map(v=>`<div class="obs-bullet"><span class="obs-bullet-dot"></span>${v}</div>`).join('')}</div><div class="obs-card"><div class="obs-card-title"><div class="obs-card-icon" style="background:rgba(168,85,247,.15);">🛡️</div><div class="obs-card-title-text">Constraints &amp; Execution Rules</div></div>${ag.constraints.map(c=>`<div class="obs-constraint-row"><div class="obs-ai-chip">AI</div><span class="obs-constraint-text">${c}</span></div>`).join('')}</div></div><div><div class="obs-card"><div class="obs-card-title"><div class="obs-card-icon" style="background:rgba(249,115,22,.15);">⚡</div><div class="obs-card-title-text">Active Model Inferences</div></div>${ag.hasInferences&&ag.inferences?ag.inferences.map(inf=>`<div class="obs-bullet"><span class="obs-bullet-dot"></span>${inf}</div>`).join(''):'<div class="obs-inference-empty">No active alerts.</div>'}</div><div class="obs-card"><div class="obs-card-title"><div class="obs-card-icon" style="background:rgba(34,197,94,.15);">📋</div><div class="obs-card-title-text">Recent Execution Log</div></div>${sampleLogs.map(l=>{const t=new Date(now-l.offset*1000);const ts=t.getHours().toString().padStart(2,'0')+':'+t.getMinutes().toString().padStart(2,'0')+':'+t.getSeconds().toString().padStart(2,'0');return `<div class="obs-log-row"><span class="obs-log-time">${ts}</span><span class="obs-log-${l.type}">${l.text}</span></div>`;}).join('')}</div></div></div>`;
}

// ── Business Rules ──
function renderBusinessRules(){
  const agEl=document.getElementById('admin-agents-list'); if(agEl) agEl.innerHTML=agentsData.map(a=>`<div class="admin-agent-row"><div><span class="admin-agent-name">${a.name}</span><span class="admin-agent-status ${a.status==='running'?'admin-status-running':'admin-status-idle'}">${a.status.toUpperCase()}</span><span class="admin-agent-version">v3.1.2</span></div><button class="admin-logs-btn" onclick="openLogs('${a.id}')"><svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="4 17 10 11 4 5"/><line x1="12" y1="19" x2="20" y2="19"/></svg>Logs</button></div>`).join('');
  const rlEl=document.getElementById('admin-rules-list'); if(rlEl) rlEl.innerHTML=adminRules.map((r,i)=>`<div class="admin-rule-row"><div><div class="admin-rule-title">${r.title}</div><div class="admin-rule-desc">${r.desc}</div>${r.editable?`<div style="margin-top:8px;display:flex;align-items:center;gap:8px;"><span style="font-size:11px;color:var(--sub);">Valor actual:</span><input class="admin-editable-input" style="width:120px;" value="${r.field==='monto'?'$'+parseInt(r.value).toLocaleString('es-MX')+' MXN':r.value+'%'}" onclick="this.select()" onblur="showToast('💾 Regla actualizada')"></div>`:''}</div><button class="admin-rule-edit" onclick="showToast('✏️ Editando: ${r.title}')"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg></button></div>`).join('');
  const pcEl=document.getElementById('admin-process-config'); if(pcEl) pcEl.innerHTML=`<div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:0;border-top:1px solid var(--border);">${processConfig.map(c=>`<div style="padding:14px 20px;border-bottom:1px solid var(--border);border-right:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;gap:12px;"><div><div style="font-size:13px;font-weight:600;color:var(--text);margin-bottom:3px;">${c.label}</div><div style="font-size:11px;color:var(--sub);">${c.desc}</div></div>${c.type==='toggle'?`<label class="admin-switch"><input type="checkbox" ${c.value?'checked':''} onchange="showToast('⚙️ ${c.label}: '+(this.checked?'ON':'OFF'))"><span class="admin-switch-slider"></span></label>`:`<input class="admin-editable-input" style="width:80px;text-align:right;" value="${c.value}" type="number" onblur="showToast('💾 Actualizado')">`}</div>`).join('')}</div>`;
}


// ── Email ──
// ══════════════════════════════════════════
//  ORACLE RETAIL PO VIEWER
// ══════════════════════════════════════════
function openOraclePOViewer(poId){
  const po = ORACLE_PO_DATA[poId];
  if(!po){ showToast('❌ PO ' + poId + ' no encontrada'); return; }

  const fmt = n => n.toLocaleString('en-US',{minimumFractionDigits:2,maximumFractionDigits:2});

  const headerHtml = (page, total=5) =>
    `<div style="display:flex;justify-content:space-between;align-items:flex-start;padding:8px 16px;border-bottom:2px solid #ccc;font-family:Arial,sans-serif;">
      <div style="display:flex;align-items:center;gap:2px;">
        <span style="color:#CC0000;font-weight:900;font-size:18px;">ORACLE</span>
        <span style="color:#555;font-size:16px;"> Retail</span>
      </div>
      <div style="text-align:center;">
        <div style="font-weight:bold;font-size:15px;">Purchase Order Report</div>
        <div style="font-size:12px;">Order No: <b>${po.orderNo}</b></div>
        <div style="font-size:12px;">FEMSA Comercio</div>
      </div>
      <div style="text-align:right;font-size:11px;color:#333;">
        <div>Report Date: 14-Apr-26</div>
        <div>Report: (ORD_DET)</div>
        <div>Page: ${page} OF ${total}</div>
      </div>
    </div>`;

  const thS = 'background:#8BAFC5;border:1px solid #6A99B5;padding:5px 8px;font-size:10.5px;font-weight:700;text-align:center;font-family:Arial;';
  const tdS = 'border:1px solid #ccc;padding:4px 8px;font-family:Arial;font-size:11px;';
  const addrLines = (po.addr||'').replace(/\\n/g,'<br>');
  const shipParts = (po.shipTo||'').split(' ');

  const vendorHtml = headerHtml(1) +
    `<div style="background:#8BAFC5;padding:12px 16px;font-family:Arial;font-size:11.5px;display:grid;grid-template-columns:1fr 1fr;gap:4px;">
      <div><b>BUYER:</b></div>
      <div style="text-align:right;"><b>NOT AFTER DATE:</b> ${po.notAfter}</div>
      <div><b>PHONE:</b></div>
      <div style="text-align:right;"><b>NOT BEFORE DATE:</b> ${po.notBefore}</div>
      <div><b>VENDOR:</b> ${po.vendor}</div><div></div>
      <div><b>VENDOR SITE:</b> ${po.site}</div>
      <div style="text-align:right;"><b>TERMS:</b> ${po.terms}</div>
      <div style="padding-left:80px;color:#222;">${addrLines}</div>
      <div style="text-align:right;"><b>DISCOUNT % APPLIED:</b> ${po.discount}</div>
      <div><b>CONTACT:</b> ${po.contact}</div>
      <div style="text-align:right;font-weight:700;">PO TOTAL COST</div>
      <div><b>PHONE:</b> ${po.phone} &nbsp;&nbsp; <b>FAX:</b> ${po.fax}</div>
      <div style="text-align:right;"><b>NET OF DISCOUNT:</b> ${po.total}</div>
      <div></div>
      <div style="text-align:right;"><b>ORDER CURRENCY:</b> MXN</div>
      <div style="grid-column:1/-1;border-top:1px solid rgba(0,0,0,.15);padding-top:4px;margin-top:4px;">
        <b>FREIGHT TERMS:</b><br><b>FOB TERMS PAY METHOD:</b><br>
        <b>TRANS. RESPONSIBILITY:</b><br><b>COMMENTS:</b> Carga Masiva RMS
      </div>
    </div>`;

  const rowsHtml = po.items.map((it,i) => {
    const bg = i%2===0?'white':'#F5F8FC';
    return `<tr style="background:${bg};">
      <td style="${tdS}text-align:center;font-weight:700;">${it.qty}</td>
      <td style="${tdS}text-align:center;">${it.pack}</td>
      <td style="${tdS}text-align:center;">${it.uop}</td>
      <td style="${tdS}">${it.desc}</td>
      <td style="${tdS}font-family:monospace;font-size:10px;">${it.item}</td>
      <td style="${tdS}text-align:center;">${it.dept}</td>
      <td style="${tdS}text-align:right;">${fmt(it.cost)}</td>
      <td style="${tdS}text-align:right;">${fmt(it.ext)}</td>
      <td style="${tdS}text-align:right;font-weight:700;">${fmt(it.ext)}</td>
    </tr>`;
  }).join('');

  const itemsHtml = headerHtml(2) +
    `<div style="background:#8BAFC5;padding:8px 16px;font-family:Arial;font-size:11.5px;display:grid;grid-template-columns:1fr 1fr;">
      <div><b>SHIP TO:</b> ${po.shipTo}<br><b>MANAGER:</b><br><b>PHONE:</b><br><b>FAX:</b></div>
      <div style="text-align:right;"><b>PO COST PER STORE</b><br><b>NET OF DISCOUNT:</b> 0.00<br><b>ORDER CURRENCY:</b></div>
    </div>
    <div style="overflow-x:auto;">
    <table style="width:100%;border-collapse:collapse;">
      <thead><tr>
        <th style="${thS}width:70px;">QUANTITY<br>ORDERED</th>
        <th style="${thS}width:70px;">PACK<br>SIZE</th>
        <th style="${thS}width:45px;">UOP</th>
        <th style="${thS}">DESCRIPTION</th>
        <th style="${thS}width:110px;">ITEM</th>
        <th style="${thS}width:75px;">DEPT</th>
        <th style="${thS}width:90px;">NET UOP<br>COST</th>
        <th style="${thS}width:95px;">VENDOR<br>EXT.COST</th>
        <th style="${thS}width:95px;">NET<br>EXT. COST</th>
      </tr></thead>
      <tbody>${rowsHtml}</tbody>
    </table></div>`;

  const summaryRows = po.items.map((it,i) => {
    const bg = i%2===0?'white':'#F5F8FC';
    return `<tr style="background:${bg};">
      <td style="${tdS}text-align:center;font-weight:700;">${it.qty}</td>
      <td style="${tdS}text-align:center;">${it.pack}</td>
      <td style="${tdS}text-align:center;">${it.uop}</td>
      <td style="${tdS}"></td>
      <td style="${tdS}">${it.desc}</td>
      <td style="${tdS}text-align:right;">${fmt(it.ext)}</td>
      <td style="${tdS}text-align:right;font-weight:700;">${fmt(it.ext)}</td>
    </tr>`;
  }).join('');

  const summaryHtml = headerHtml(4) +
    `<div style="background:#8BAFC5;padding:4px 16px;font-family:Arial;font-size:11px;display:flex;justify-content:space-between;">
      <b>SUMMARY – TOTAL ALL STORES</b><b>ORDER CURRENCY: MXN</b>
    </div>
    <table style="width:100%;border-collapse:collapse;">
      <thead><tr>
        <th style="${thS}width:70px;">QUANTITY<br>ORDERED</th>
        <th style="${thS}width:70px;">PACK<br>SIZE</th>
        <th style="${thS}width:45px;">UOP</th>
        <th style="${thS}width:80px;">REF ITEM</th>
        <th style="${thS}">DESCRIPTION</th>
        <th style="${thS}width:105px;">TOTAL VENDOR<br>EXT. COST</th>
        <th style="${thS}width:105px;">TOTAL NET<br>EXT. COST</th>
      </tr></thead>
      <tbody>${summaryRows}</tbody>
    </table>
    <div style="padding:12px 16px;font-family:Arial;font-size:10.5px;line-height:1.8;border-top:1px solid #ccc;margin-top:8px;">
      THIS ORDER IS PLACED BY BUYER SUBJECT TO THE TERMS AND CONDITIONS APPEARING HEREON.<br>
      1. EACH LOCATION RECEIVING MERCHANDISE MUST BE INVOICED SEPARATELY.<br>
      2. ORIGINAL INVOICE TO THE OFFICE LISTED ABOVE.<br>
      3. COPY OF INVOICE, OR PRICED PACKING SLIP, MUST ACCOMPANY THE SHIPMENT TO THE STORE.<br>
      4. OUR P.O. NUMBERS MUST APPEAR ON ALL DOCUMENTS PERTAINING TO THIS ORDER.<br>
      5. NO BACK ORDERS OR SUBSTITUTIONS WITHOUT AUTHORIZATION.
    </div>`;

  const signHtml = headerHtml(5) +
    `<div style="padding:48px 16px;font-family:Arial;font-size:12px;text-align:center;">
      <div style="display:inline-block;border-top:1px solid #333;padding-top:6px;width:200px;">AUTHORIZED SIGNATURE</div>
      <p style="font-weight:700;margin-top:24px;">End of Report</p>
    </div>`;

  const tabs = [
    {label:'Pg 1 — Vendor Info', html: vendorHtml},
    {label:`Pg 2 — Items (${po.items.length})`, html: itemsHtml},
    {label:'Pg 4 — Summary', html: summaryHtml},
    {label:'Pg 5 — Firma', html: signHtml}
  ];

  const tabBtns = tabs.map((t,i) =>
    `<button onclick="oracleSwitchTab(${i})" id="otab-${i}" style="padding:8px 16px;font-family:Arial;font-size:12px;border:1px solid #8BAFC5;border-bottom:${i===0?'2px solid white':'1px solid #8BAFC5'};background:${i===0?'white':'#EEF4FA'};color:#003366;cursor:pointer;margin-bottom:-1px;border-radius:3px 3px 0 0;">${t.label}</button>`
  ).join('');

  const outerHtml =
    `<div style="font-family:Arial;background:white;min-height:600px;">
      <div style="display:flex;align-items:center;gap:12px;padding:12px 16px;background:#F5F8FC;border-bottom:2px solid #8BAFC5;">
        <div style="display:flex;align-items:center;gap:4px;">
          <span style="color:#CC0000;font-weight:900;font-size:22px;">ORACLE</span>
          <span style="color:#555;font-size:18px;"> Retail</span>
        </div>
        <div style="flex:1;text-align:center;">
          <span style="font-weight:700;color:#003366;font-size:14px;">Purchase Order Report — Orden ${po.orderNo}</span><br>
          <span style="font-size:11px;color:#666;">FEMSA Comercio | 14-Apr-26 | ${po.location} | Total: $${po.total} MXN</span>
        </div>
        <div style="background:#CC0000;color:white;padding:4px 10px;border-radius:4px;font-size:11px;font-weight:700;">${po.items.length} SKUs</div>
      </div>
      <div style="padding:0 0 0 0;border-bottom:1px solid #8BAFC5;display:flex;gap:2px;padding-left:12px;padding-top:8px;background:#EEF4FA;">
        ${tabBtns}
      </div>
      <div id="oracle-tab-content" style="overflow:auto;max-height:65vh;">${tabs[0].html}</div>
    </div>`;

  window._oracleTabs = tabs;
  const body = document.getElementById('po-modal-body');
  if(body) body.innerHTML = outerHtml;
  openModal('modal-po');
}

function oracleSwitchTab(i){
  var tabs = window._oracleTabs || [];
  var content = document.getElementById('oracle-tab-content');
  if(content && tabs[i]) content.innerHTML = tabs[i].html;
  // Update tab styling
  for(var j=0;j<tabs.length;j++){
    var btn = document.getElementById('otab-'+j);
    if(btn){
      btn.style.background = j===i ? 'white' : '#EEF4FA';
      btn.style.borderBottom = j===i ? '2px solid white' : '1px solid #8BAFC5';
    }
  }
}

// Excel summary viewer
function openExcelSummaryViewer(){
  var rows = [
    ['76933176','15AGU','SERVICIOS ADMINISTRATIVOS','Aguascalientes','22-Apr-2026','143,544.11'],
    ['76933072','15TQV','SERVICIOS ADMINISTRATIVOS','Querétaro','20-Apr-2026','348,257.85'],
    ['76933173','15VCZ','SERVICIOS ADMINISTRATIVOS','Veracruz','21-Apr-2026','300,534.58'],
    ['76933065','15OBQ','SERVICIOS ADMINISTRATIVOS','Cd. Obregón','21-Apr-2026','533,410.72'],
    ['76933070','15VHD','SERVICIOS ADMINISTRATIVOS','Villahermosa','22-Apr-2026','464,327.87'],
    ['76933175','15GUA','SERVICIOS ADMINISTRATIVOS','Tlajomulco GDL','21-Apr-2026','581,443.84']
  ];
  var thS = 'background:#217346;color:white;padding:8px 12px;font-family:Calibri,Arial;font-size:12px;font-weight:700;border:1px solid #1a5c38;white-space:nowrap;';
  var tdS = 'padding:7px 12px;font-family:Calibri,Arial;font-size:12px;border:1px solid #D0D0D0;';
  var total = rows.reduce(function(s,r){ return s + parseFloat(r[5].replace(/,/g,'')); }, 0);
  var html =
    '<div style="background:#217346;color:white;padding:12px 20px;font-family:Calibri,Arial;">' +
      '<div style="font-size:16px;font-weight:700;">RESUMEN OC — SERVICIOS ADMINISTRATIVOS 2026</div>' +
      '<div style="font-size:12px;opacity:.85;">Carga Masiva RMS | FEMSA Comercio | Vendor: 101041 | Reporte: 14-Abr-2026</div>' +
    '</div>' +
    '<div style="overflow-x:auto;padding:16px;">' +
    '<table style="width:100%;border-collapse:collapse;">' +
      '<thead><tr>' +
        '<th style="'+thS+'">Order No</th>' +
        '<th style="'+thS+'">Vendor Site</th>' +
        '<th style="'+thS+'">Descripción</th>' +
        '<th style="'+thS+'">Ship To</th>' +
        '<th style="'+thS+'">Not After Date</th>' +
        '<th style="'+thS+'text-align:right;">Total MXN</th>' +
      '</tr></thead>' +
      '<tbody>' +
      rows.map(function(r,i){
        var bg = i%2===0?'white':'#EAF3EC';
        return '<tr style="background:'+bg+';">' +
          r.slice(0,5).map(function(c){ return '<td style="'+tdS+'">'+c+'</td>'; }).join('') +
          '<td style="'+tdS+'text-align:right;font-weight:700;color:#217346;">$'+r[5]+'</td>' +
        '</tr>';
      }).join('') +
      '<tr style="background:#D6E8D6;font-weight:700;">' +
        '<td style="'+tdS+'" colspan="5"><b>TOTAL CONSOLIDADO (6 OCs)</b></td>' +
        '<td style="'+tdS+'text-align:right;color:#217346;font-size:14px;font-weight:900;">$'+total.toLocaleString('en-US',{minimumFractionDigits:2})+'</td>' +
      '</tr>' +
      '</tbody>' +
    '</table>' +
    '<div style="margin-top:16px;padding:12px;background:#EAF3EC;border-radius:6px;font-family:Calibri;font-size:11.5px;color:#333;">' +
      '<b>ORDER CURRENCY:</b> MXN &nbsp;|&nbsp; <b>TERMS:</b> 30 días &nbsp;|&nbsp; ' +
      '<b>CONTACT:</b> PRECIADO NORA &nbsp;|&nbsp; <b>PHONE:</b> 6622890740 &nbsp;|&nbsp; ' +
      '<b>COMMENTS:</b> Carga Masiva RMS' +
    '</div>' +
    '</div>';
  var body = document.getElementById('po-modal-body');
  if(body) body.innerHTML = html;
  openModal('modal-po');
}


function renderEmails(){
  const el = document.getElementById('email-list-body');
  if(!el) return;
  el.innerHTML = emailsData.map(e => {
    const isUnread = e.unread === true || e.read === false;
    const isActive = activeEmailId === e.id;
    return `<div class="email-item ${isUnread?'unread':''} ${isActive?'active':''}" onclick="openEmail('${e.id}')" id="eitem-${e.id}">
      ${isUnread?'<span class="unread-dot"></span>':''}
      <div class="email-item-from"><span>${e.fromName||e.from}</span><span class="email-item-time">${e.time}</span></div>
      <div class="email-item-subject">${e.subject}</div>
      <div class="email-item-preview">${e.preview||''}</div>
    </div>`;
  }).join('');
}

function filterEmails(q){
  document.querySelectorAll('.email-item').forEach(el=>{el.style.display=el.textContent.toLowerCase().includes(q.toLowerCase())?'':'none';});
}

function openEmail(id){
  activeEmailId = id;
  const email = emailsData.find(e => e.id === id);
  if(!email) return;
  // Mark as read
  email.read = true;
  email.unread = false;
  renderEmails();

  const panel = document.getElementById('email-panel') || document.getElementById('email-detail-content');
  if(!panel) return;

  const isOraclePO = email.tag === 'oc' || email.tag === 'urgente';
  const isError    = email.tag === 'error';

  // ── Body ──
  let bodyHtml;
  if(email.body && email.body.trim().startsWith('<')){
    bodyHtml = email.body; // already HTML
  } else {
    const raw = email.body || mkEmailBody(email.area||'');
    bodyHtml = '<pre style="font-family:Arial;font-size:13px;white-space:pre-wrap;line-height:1.7;color:#222;">' + raw + '</pre>';
  }

  // ── Attachments ──
  let attHtml = '';
  if(email.attachments && email.attachments.length){
    const icons = {
      pdf: '<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#CC0000" stroke-width="2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14,2 14,8 20,8"/></svg>',
      xlsx:'<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#217346" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2"/><line x1="3" y1="9" x2="21" y2="9"/><line x1="3" y1="15" x2="21" y2="15"/><line x1="9" y1="3" x2="9" y2="21"/></svg>'
    };
    attHtml = '<div style="border-top:1px solid var(--border);padding:12px 20px;background:var(--light);display:flex;gap:10px;flex-wrap:wrap;">';
    email.attachments.forEach(att => {
      const ic = icons[att.type] || icons.pdf;
      const poKey = att.poRef || att.poId;
      let clickFn;
      if(poKey && ORACLE_PO_DATA[poKey]){
        clickFn = `openOraclePOViewer('${poKey}')`;
      } else if(att.type === 'xlsx'){
        clickFn = `openExcelSummaryViewer()`;
      } else {
        clickFn = `showToast('📎 Descargando: ${att.name}')`;
      }
      attHtml +=
        `<div onclick="${clickFn}" style="display:flex;align-items:center;gap:8px;padding:8px 14px;background:white;border:1.5px solid var(--border);border-radius:10px;cursor:pointer;transition:border-color .2s;font-size:12.5px;" onmouseover="this.style.borderColor='var(--orange)'" onmouseout="this.style.borderColor='var(--border)'">
          ${ic}
          <div>
            <div style="font-weight:600;color:var(--text);">${att.name}</div>
            <div style="font-size:10.5px;color:var(--sub);">${att.size} — click para ver</div>
          </div>
        </div>`;
    });
    attHtml += '</div>';
  }

  const tagBadge = isOraclePO
    ? '<div style="margin-left:auto;display:flex;align-items:center;gap:5px;background:#FFF5F5;border:1px solid #FCA5A5;padding:4px 10px;border-radius:8px;"><span style="color:#CC0000;font-weight:900;font-size:13px;">ORACLE</span><span style="color:#555;font-size:12px;"> Retail</span></div>'
    : isError
      ? '<div style="margin-left:auto;background:#FFF1F0;border:1px solid #FCA5A5;padding:4px 10px;border-radius:8px;font-size:11px;font-weight:700;color:#CC0000;">⚠ ERROR SAP</div>'
      : '';

  panel.innerHTML =
    `<div style="padding:16px 20px;border-bottom:1px solid var(--border);background:white;">
      <div style="font-size:16px;font-weight:700;color:var(--text);margin-bottom:8px;">${email.subject}</div>
      <div style="display:flex;align-items:center;gap:12px;font-size:12.5px;">
        <div style="background:var(--orange);color:white;border-radius:20px;padding:2px 10px;font-size:11px;font-weight:700;">${(email.fromName||'?').charAt(0).toUpperCase()}</div>
        <div>
          <div style="font-weight:600;color:var(--text);">${email.fromName||email.from}</div>
          <div style="color:var(--sub);">Para: ${email.to||'pedidos@caffenio.com'} | ${email.date} ${email.time}</div>
        </div>
        ${tagBadge}
      </div>
    </div>
    <div style="flex:1;overflow-y:auto;padding:20px 24px;background:white;">${bodyHtml}</div>
    ${attHtml}
    <div style="padding:10px 20px;border-top:1px solid var(--border);display:flex;gap:8px;background:var(--light);">
      <button class="btn btn-orange" onclick="showToast('↩ Respuesta enviada')">↩ Responder</button>
      <button class="btn btn-ghost" onclick="showToast('✉ Reenviado')">→ Reenviar</button>
      ${isOraclePO ? '<button class="btn btn-dark" onclick="showToast(\'⚡ Procesando en SAP SD…\')"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="5 3 19 12 5 21 5 3"/></svg> Procesar en SAP</button>' : ''}
    </div>`;
}



// ════════════════════════════════════════════
//  INIT
// ════════════════════════════════════════════
// Modal click-outside to close
// ════════════════════════════════════════════════════════════════════
//  MISSING DATA — agentsData, adminRules, processConfig
// ════════════════════════════════════════════════════════════════════
const agentsData = [
  {id:'ag01',name:'Email Classifier',status:'running',confidence:94,impact:'High',rate:98,
   purpose:'NLP classification of incoming emails. Extracts Oracle Retail PO metadata (order no, vendor site, amounts) using regex + ML. Routes to SAP SD pipeline.',
   dataVectors:['Email sender whitelist (KNA1)','Subject line pattern matching','Attachment type detection (PDF/XLSX)','Oracle Retail ORD_DET format parsing'],
   constraints:['Only processes @oxxo.com.mx and @femsa.com senders','Requires PDF attachment to trigger PO flow','Max 50 emails/minute throughput'],
   hasInferences:true,
   inferences:['High confidence match: 76933175 → po-gua (99.2%)','Vendor 101041 pattern recognized across 6 OCs','Predicted delivery window: 14-22 Apr 2026']},
  {id:'ag02',name:'SAP SD Automator',status:'running',confidence:91,impact:'High',rate:95,
   purpose:'Creates Sales Orders (VA01) via BAPI_SALESORDER_CREATEFROMDAT2. Maps Oracle Retail PO items to SAP material masters. Handles currency/UOM conversions.',
   dataVectors:['ORACLE_PO_DATA item catalog','CAFFENIO_PRODUCTS SKU mapping','SAP plant CAF1 material masters','Customer account group OXXO'],
   constraints:['Plant CAF1 only','MXN currency enforced','Requires valid material in MARA','Auto-blocks on BAPI error'],
   hasInferences:true,
   inferences:['Material PKG-602 missing in CAF1 — blocked OC 76933065','Estimated auto-process rate: 5 of 6 OCs (83%)','SLA risk: 76933072 expires 20-Apr']},
  {id:'ag03',name:'Delivery Planner',status:'running',confidence:88,impact:'Medium',rate:97,
   purpose:'Generates VL01N delivery documents from confirmed Sales Orders. Assigns picking locations (SLOC), batch numbers, and transport routes.',
   dataVectors:['OXXO_STORES address catalog','Route master data','Storage location 0001/0002/0004','GI posting calendar'],
   constraints:['GI date ≥ order date','Weight validation required','Back-orders require manual approval'],
   hasInferences:false,inferences:[]},
  {id:'ag04',name:'Error Recovery Agent',status:'error',confidence:72,impact:'High',rate:78,
   purpose:'Monitors BAPI errors and SAP exception logs. Attempts automatic remediation via fuzzy SKU matching and customer alias resolution.',
   dataVectors:['ERR_CODES catalog','Material master fuzzy index','Customer alias table','Historical error patterns'],
   constraints:['Max 3 retry attempts','Human approval required for material creation','Cannot modify price conditions'],
   hasInferences:true,
   inferences:['ERROR d70f20b4: PKG-602 not in plant CAF1','Fuzzy match failed — no similar SKU found','Escalation required: manual MM01 creation']},
  {id:'ag05',name:'KPI Monitor',status:'running',confidence:96,impact:'Medium',rate:100,
   purpose:'Real-time aggregation of OTC pipeline metrics. Computes SLA compliance, error rates, processing velocity. Feeds Control Tower dashboard.',
   dataVectors:['All order lifecycle events','TEN_DAYS volume series','Error rate by type','Processing time log'],
   constraints:['Read-only — no write access to SAP','15-second refresh cycle','Alert threshold: error rate > 5%'],
   hasInferences:false,inferences:[]}
];

const adminRules = [
  {title:'Auto-aprobación de OCs < umbral',desc:'Órdenes de Compra por debajo del monto configurado se aprueban y procesan automáticamente sin intervención humana.',editable:true,field:'monto',value:'500000'},
  {title:'Whitelist de remitentes confiables',desc:'Solo se procesan correos de dominios @oxxo.com.mx, @femsa.com y @emeal.nttdata.com. Resto requiere revisión manual.',editable:false},
  {title:'Reintento automático en error SAP',desc:'En caso de fallo BAPI, el sistema reintenta hasta 3 veces con backoff exponencial (30s, 2min, 10min) antes de escalar.',editable:true,field:'pct',value:'3'},
  {title:'Ventana de procesamiento nocturno',desc:'Lote batch nocturno ejecuta de 02:00 a 05:00 para reprocesar pedidos pendientes y sincronizar inventario.',editable:false},
  {title:'Alerta de SLA por vencimiento',desc:'Se genera alerta automática cuando una OC tiene menos de 48 horas para su fecha "Not After". Prioridad alta.',editable:true,field:'pct',value:'48'},
  {title:'Modo de aprendizaje activo',desc:'El Email Classifier registra todas las correcciones manuales para re-entrenamiento semanal del modelo NLP.',editable:false}
];

const processConfig = [
  {label:'Auto-procesamiento',desc:'Crear SO automáticamente al detectar OC válida',type:'toggle',value:true},
  {label:'Notificaciones email',desc:'Enviar confirmación al proveedor tras cada SO',type:'toggle',value:true},
  {label:'Validación de stock',desc:'Verificar disponibilidad en CAF1 antes de crear SO',type:'toggle',value:true},
  {label:'Modo debug',desc:'Log detallado de todas las operaciones BAPI',type:'toggle',value:false},
  {label:'Batch size',desc:'Máximo de OCs a procesar por ciclo',type:'number',value:10},
  {label:'Timeout BAPI (seg)',desc:'Tiempo límite para llamadas RFC a SAP',type:'number',value:30},
  {label:'Reintentos máx.',desc:'Intentos antes de escalar a operaciones',type:'number',value:3},
  {label:'SLA alerta (hrs)',desc:'Horas antes de vencimiento para activar alerta',type:'number',value:48}
];

// ════════════════════════════════════════════════════════════════════
//  CORE UI FUNCTIONS
// ════════════════════════════════════════════════════════════════════

function navigate(section){
  document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  const view = document.getElementById('view-' + section);
  const nav  = document.getElementById('nav-' + section);
  if(view) view.classList.add('active');
  if(nav)  nav.classList.add('active');
  // Trigger renders
  const renders = {
    'email-inbox': () => renderEmails(),
    'lifecycle': () => initLifecycle(),
    'control-tower': () => renderControlTower(),
    'agent-observatory': () => renderObservatory(),
    'business-rules': () => renderBusinessRules(),
    'repositorio': () => renderRepositorio()
  };
  if(renders[section]) renders[section]();
}

function openModal(id){
  const m = document.getElementById(id);
  if(m) m.classList.add('open');
}

function closeModal(id){
  const m = document.getElementById(id);
  if(m) m.classList.remove('open');
}

function showToast(msg){
  let t = document.getElementById('_toast');
  if(!t){
    t = document.createElement('div');
    t.id = '_toast';
    t.style.cssText = 'position:fixed;bottom:28px;right:28px;background:#1E293B;color:white;padding:12px 20px;border-radius:12px;font-size:13.5px;font-family:var(--font,Arial);z-index:99999;box-shadow:0 4px 20px rgba(0,0,0,.25);transition:opacity .3s;opacity:0;pointer-events:none;max-width:360px;';
    document.body.appendChild(t);
  }
  t.textContent = msg;
  t.style.opacity = '1';
  clearTimeout(t._timer);
  t._timer = setTimeout(() => { t.style.opacity = '0'; }, 2800);
}

// ══════════════════════════════════════════════════════════
//  LIFECYCLE — Filters, Tabs, Render
// ══════════════════════════════════════════════════════════
let _lcDayFilter   = '';   // 'YYYY-MM-DD' or ''
let _lcMonthFilter = '';   // '04' or ''
let _lcSearchQ     = '';
let _lcPage        = 1;
let _lcActiveTab   = 'backlog';
const _lcPageSize  = 15;

// Warn correction state
let _warnTargetId  = null;
let _warnSelected  = null;

// Filter helpers
function _lcApplyFilters(rows){
  let r = rows;
  if(_lcDayFilter){
    // convert day.d = 'DD/MM/YYYY' to compare with 'YYYY-MM-DD'
    const [fy,fm,fd] = _lcDayFilter.split('-');
    const target = fd+'/'+fm+'/'+fy;
    r = r.filter(o => o.date === target);
  }
  if(_lcMonthFilter){
    r = r.filter(o => o.date.split('/')[1] === _lcMonthFilter);
  }
  if(_lcSearchQ){
    const q = _lcSearchQ.toLowerCase();
    r = r.filter(o =>
      (o.sapNum||'').includes(_lcSearchQ) ||
      (o.fromName||'').toLowerCase().includes(q) ||
      (o.poNumber||'').toLowerCase().includes(q) ||
      (o.items||[]).some(it => it.sku.toLowerCase().includes(q) || it.desc.toLowerCase().includes(q))
    );
  }
  return r;
}

function setLCFilterAll(){
  _lcDayFilter   = '';
  _lcMonthFilter = '';
  _lcPage        = 1;
  const di = document.getElementById('lc-day-input');
  const ms = document.getElementById('lc-month-sel');
  if(di) di.value = '';
  if(ms) ms.value = '';
  renderLCTable();
}
function setLCDayFilter(v){
  _lcDayFilter = v; _lcMonthFilter = ''; _lcPage = 1;
  const ms = document.getElementById('lc-month-sel');
  if(ms) ms.value = '';
  renderLCTable();
}
function setLCMonthFilter(v){
  _lcMonthFilter = v; _lcDayFilter = ''; _lcPage = 1;
  const di = document.getElementById('lc-day-input');
  if(di) di.value = '';
  renderLCTable();
}
function setLCDate(d){
  // Legacy compatibility (Control Tower clicks)
  if(d==='all'){ setLCFilterAll(); } else { setLCDayFilter(d.split('/').reverse().join('-')); }
}
function setLCSearch(q){ _lcSearchQ = q; _lcPage = 1; renderLCTable(); }

function switchTab(tab){
  ['backlog','success','errors'].forEach(t => {
    const panel = document.getElementById('panel-' + t);
    const btn   = document.getElementById('tab-' + t);
    if(panel) panel.style.display = t === tab ? '' : 'none';
    if(btn)   btn.classList.toggle('active', t === tab);
  });
  _lcActiveTab = tab;
  _lcPage = 1;
  renderLCTable();
}

// ── Item summary text ───────────────────────────────────────
function _itemSummary(items){
  if(!items||!items.length) return '—';
  const names = items.map(it => it.desc.replace('Café ','CAFÉ ').replace('Cafe ','CAFÉ ').replace('Leche ','LECHE ').replace('Azúcar ','AZÚCAR ').replace('Azucar ','AZÚCAR ').replace('Vaso ','VASO ').replace('Tapa ','TAPA ').replace('Sacarina','SAC.').toUpperCase().split(' ').slice(0,2).join(' '));
  const total = items.reduce((s,it)=>s+it.total,0);
  const summary = names.slice(0,3).join(' + ') + (names.length>3?'…':'');
  const fmtMXN = total.toLocaleString('es-MX',{minimumFractionDigits:0,maximumFractionDigits:0});
  return `<div style="font-size:12.5px;font-weight:600;color:var(--text);line-height:1.4;">${summary.length>42?summary.substring(0,42)+'…':summary}</div>
    <div style="font-size:11px;color:var(--sub);margin-top:2px;">${items.length} SKU${items.length>1?'s':''} / <span style="font-weight:700;color:var(--text);">$${fmtMXN} MXN</span></div>`;
}

// ── Process order → Success ─────────────────────────────────
function processOrder(sapNum){
  if(!window.DATASET) return;
  const o = DATASET.all.find(x => x.sapNum === sapNum);
  if(!o || o.status !== 'backlog') return;
  o.status    = 'success';
  o.subStatus = null;
  o.soNumber  = 'SO-' + String(1000000 + parseInt(sapNum.slice(-6))).toString().padStart(9,'0');
  o.processingTime = Math.round((0.8 + Math.random() * 4) * 10) / 10;
  // Rebuild DATASET subsets
  DATASET.success = DATASET.all.filter(x=>x.status==='success');
  DATASET.backlog  = DATASET.all.filter(x=>x.status==='backlog');
  DATASET.errors   = DATASET.all.filter(x=>x.status==='error');
  window.backlogData = DATASET.backlog;
  window.errorsData  = DATASET.errors;
  showToast('✅ SO creada: ' + o.soNumber + ' — Orden procesada en SAP SD');
  renderLCTable();
}

// ── Warn correction modal ───────────────────────────────────
const WARN_CORRECTIONS = {
  'default': [
    { id:'w1', icon:'🤖', label:'Auto-corrección IA',
      desc:'El agente corrige el mapeo de cliente y reintenta la creación de la orden en SAP SD automáticamente.',
      detail:'Confianza: 94% · Tiempo estimado: ~45 seg · Sin intervención humana requerida' },
    { id:'w2', icon:'🔧', label:'Corrección manual + Procesar',
      desc:'Abre el formulario de revisión para ajustar datos del pedido (SKU, cantidad, cliente) antes de enviar a SAP.',
      detail:'Requiere 2-5 min · Garantiza datos correctos · Trazabilidad completa' },
    { id:'w3', icon:'⏸', label:'Diferir para revisión posterior',
      desc:'Marca el pedido como revisión pendiente y notifica al equipo de operaciones por email.',
      detail:'SLA: revisar en ≤4 hrs · Se agrega a cola de revisión · Genera ticket automático' }
  ],
  'MAT-SKU-404': [
    { id:'w1', icon:'🔄', label:'Fuzzy-match de SKU',
      desc:'El agente busca el material más similar en el maestro MARA usando similitud de nombre y características.',
      detail:'Confianza: 87% · Base: MARA CAF1 · Propuesta: sustituir por material equivalente' },
    { id:'w2', icon:'📦', label:'Crear material en MM01',
      desc:'Solicitar creación urgente del material PKG-602 en la planta CAF1 con tipo FERT.',
      detail:'Requiere autorización Materiales · Tiempo: 2-4 hrs · Bloquea OC hasta resolución' },
    { id:'w3', icon:'⏸', label:'Diferir — Notificar Compras',
      desc:'Enviar alerta a gerencia de compras y bloquear la OC hasta que el material esté disponible en el sistema.',
      detail:'SLA: resolución en ≤24 hrs · Se genera ticket Jira automático · Notificación a Rommel Gil' }
  ]
};

function openWarnModal(sapNum){
  _warnTargetId = sapNum;
  _warnSelected = null;
  const o = DATASET.all.find(x => x.sapNum === sapNum);
  if(!o) return;
  const sub  = document.getElementById('warn-modal-sub');
  const info = document.getElementById('warn-modal-info');
  const cont = document.getElementById('warn-options-container');
  const btn  = document.getElementById('warn-apply-btn');
  const corrKey = o.errorCode || 'default';
  const opts = WARN_CORRECTIONS[corrKey] || WARN_CORRECTIONS['default'];
  if(sub)  sub.textContent  = `Orden ${o.poNumber} · ${o.fromName}`;
  if(info) info.innerHTML   = `<b>⚠ Anomalía detectada:</b> ${o.errorCode||'Validación fallida'} · <b>Total:</b> $${(o.totalMXN||0).toLocaleString('es-MX')} MXN · <b>Tienda:</b> ${o.fromName}`;
  if(cont) cont.innerHTML   = opts.map((opt,i) => `
    <div class="warn-option" id="wopt-${i}" onclick="selectWarnOption(${i}, '${opt.id}')">
      <div style="display:flex;align-items:flex-start;gap:12px;">
        <span style="font-size:22px;flex-shrink:0;">${opt.icon}</span>
        <div style="flex:1;">
          <div style="font-size:13.5px;font-weight:700;color:var(--text);margin-bottom:4px;">${opt.label}</div>
          <div style="font-size:12px;color:var(--sub);line-height:1.5;">${opt.desc}</div>
          <div style="margin-top:6px;font-size:11px;font-family:var(--mono);background:var(--light);border-radius:6px;padding:5px 8px;color:var(--sub);">${opt.detail}</div>
        </div>
        <div style="width:20px;height:20px;border-radius:50%;border:2px solid var(--border);flex-shrink:0;margin-top:2px;display:flex;align-items:center;justify-content:center;" id="wopt-radio-${i}"></div>
      </div>
    </div>`).join('');
  if(btn){ btn.disabled=true; btn.style.opacity='.5'; }
  openModal('modal-warn-correction');
}

function selectWarnOption(idx, optId){
  _warnSelected = optId;
  document.querySelectorAll('.warn-option').forEach((el,i) => {
    el.classList.toggle('selected', i===idx);
    const radio = document.getElementById('wopt-radio-'+i);
    if(radio) radio.innerHTML = i===idx ? '<div style="width:10px;height:10px;border-radius:50%;background:var(--orange);"></div>' : '';
    if(radio && i===idx) radio.style.borderColor='var(--orange)'; else if(radio) radio.style.borderColor='var(--border)';
  });
  const btn = document.getElementById('warn-apply-btn');
  if(btn){ btn.disabled=false; btn.style.opacity='1'; }
}

function applyWarnCorrection(){
  if(!_warnTargetId || !_warnSelected) return;
  closeModal('modal-warn-correction');
  const o = DATASET.all.find(x => x.sapNum === _warnTargetId);
  if(!o) return;
  if(_warnSelected === 'w1'){
    // Auto-correct → process to success
    setTimeout(() => processOrder(_warnTargetId), 800);
    showToast('🤖 Agente aplicando corrección automática…');
  } else if(_warnSelected === 'w2'){
    showToast('🔧 Abriendo formulario de corrección manual…');
    setTimeout(() => { processOrder(_warnTargetId); showToast('✅ Pedido corregido y procesado'); }, 1800);
  } else {
    o.subStatus = 'deferred';
    showToast('⏸ Pedido diferido — Notificación enviada a operaciones');
    renderLCTable();
  }
  _warnTargetId = null; _warnSelected = null;
}

// ── Main render ─────────────────────────────────────────────
function renderLCTable(){
  if(!window.DATASET) return;
  const base = _lcApplyFilters(DATASET.all);
  const total   = base.length;
  const success = base.filter(o=>o.status==='success').length;
  const backlog = base.filter(o=>o.status==='backlog').length;
  const errors  = base.filter(o=>o.status==='error').length;

  const setEl = (id,v) => { const e=document.getElementById(id); if(e) e.textContent=v; };
  setEl('cnt-all',     total.toLocaleString());
  setEl('cnt-success', success.toLocaleString());
  setEl('cnt-backlog', backlog.toLocaleString());
  setEl('cnt-errors',  errors.toLocaleString());
  setEl('tc-backlog',  backlog);
  setEl('tc-success',  success);
  setEl('tc-errors',   errors);
  // Todos pill count
  const pcount = document.getElementById('lc-pill-count');
  if(pcount) pcount.textContent = total.toLocaleString();

  const fmt = n => n.toLocaleString('es-MX',{minimumFractionDigits:0,maximumFractionDigits:0});

  const panels = {
    backlog:{
      rows: base.filter(o=>o.status==='backlog'),
      el:'backlog-rows',
      rowFn: o => {
        const isWarn = o.subStatus==='warn' || o.subStatus==='deferred';
        const badgeHtml = isWarn
          ? `<span class="lc-badge lc-badge-warn"><svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"/></svg>WARN</span>`
          : `<span class="lc-badge lc-badge-pending"><svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>PENDING</span>`;
        const actionBtn = isWarn
          ? `<button class="btn-warn" onclick="openWarnModal('${o.sapNum}')"><svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"/><line x1="12" y1="9" x2="12" y2="13"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg>Advertencia</button>`
          : `<button class="btn-sap" onclick="processOrder('${o.sapNum}')"><svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="5 12 12 5 19 12"/><polyline points="5 19 12 12 19 19"/></svg>→SAP</button>`;
        return `<div class="table-row grid-backlog">
          <span><input type="checkbox" class="lc-check"></span>
          <span>
            <div style="font-weight:700;font-size:13px;color:var(--text);">${o.fromName.replace('OXXO ','OXXO ')}</div>
            <div style="font-size:10.5px;font-family:var(--mono);color:var(--sub);margin-top:2px;">${o.poNumber}</div>
          </span>
          <span>
            <div style="font-size:12.5px;color:var(--text);">${o.date.split('/').reverse().join('/')}</div>
            <div style="font-size:11px;color:var(--sub);">${o.recvTime||'09:14'}</div>
          </span>
          <span>${_itemSummary(o.items)}</span>
          <span>${badgeHtml}</span>
          <span style="display:flex;gap:6px;align-items:center;flex-wrap:wrap;">
            <button class="btn-detail" onclick="showToast('📋 Detalle: ${o.poNumber}')">Detalle</button>
            ${actionBtn}
            <button class="btn-kebab" onclick="showToast('⋮ Más opciones')">⋮</button>
          </span>
        </div>`;
      }
    },
    success:{
      rows: base.filter(o=>o.status==='success'),
      el:'success-rows',
      rowFn: o => `<div class="table-row grid-success">
        <span><input type="checkbox" class="lc-check"></span>
        <span>
          <div style="font-weight:700;font-size:13px;color:var(--text);">${o.fromName}</div>
          <div style="font-size:10.5px;font-family:var(--mono);color:var(--sub);margin-top:2px;">${o.poNumber}</div>
        </span>
        <span>
          <div style="font-size:12.5px;">${o.date.split('/').reverse().join('/')}</div>
          <div style="font-size:11px;color:var(--sub);">${o.recvTime||'—'}</div>
        </span>
        <span>${_itemSummary(o.items)}</span>
        <span><span class="lc-badge lc-badge-success">✓ Procesado</span></span>
        <span style="font-family:var(--mono);font-size:12px;font-weight:700;color:#16A34A;">${o.soNumber||'—'}</span>
        <span style="display:flex;gap:6px;align-items:center;">
          <button class="btn-detail" onclick="showToast('📋 SO: ${o.soNumber||o.sapNum}')">Detalle</button>
          <span style="font-size:11px;color:var(--sub);">${o.processingTime}min</span>
        </span>
      </div>`
    },
    errors:{
      rows: base.filter(o=>o.status==='error'),
      el:'errors-rows',
      rowFn: o => `<div class="table-row grid-errors">
        <span><input type="checkbox" class="lc-check"></span>
        <span>
          <div style="font-weight:700;font-size:13px;color:var(--text);">${o.fromName}</div>
          <div style="font-size:10.5px;font-family:var(--mono);color:var(--sub);margin-top:2px;">${o.poNumber}</div>
        </span>
        <span>
          <div style="font-size:12.5px;">${o.date.split('/').reverse().join('/')}</div>
          <div style="font-size:11px;color:var(--sub);">${o.recvTime||'—'}</div>
        </span>
        <span>${_itemSummary(o.items)}</span>
        <span>
          <span class="lc-badge lc-badge-error">✗ Error</span>
          <div style="font-size:10.5px;font-family:var(--mono);color:#DC2626;margin-top:4px;">${o.errorCode||'—'}</div>
        </span>
        <span style="font-family:var(--mono);font-size:11px;">—</span>
        <span style="display:flex;gap:6px;align-items:center;flex-wrap:wrap;">
          <button class="btn-detail" onclick="showToast('📋 Error: ${o.errorCode||'—'}')">Detalle</button>
          <button class="btn-warn" onclick="openWarnModal('${o.sapNum}')">Fix</button>
        </span>
      </div>`
    }
  };

  Object.entries(panels).forEach(([tab, cfg]) => {
    const el = document.getElementById(cfg.el);
    if(!el) return;
    const totalR = cfg.rows.length;
    const totalP = Math.ceil(totalR / _lcPageSize) || 1;
    const pg     = Math.min(_lcPage, totalP);
    const paged  = cfg.rows.slice((pg-1)*_lcPageSize, pg*_lcPageSize);
    el.innerHTML = paged.length
      ? paged.map(cfg.rowFn).join('')
      : `<div style="padding:48px;text-align:center;color:var(--sub);">
          <div style="font-size:32px;margin-bottom:8px;">🎉</div>
          <div style="font-weight:600;">No hay registros para este filtro</div>
         </div>`;
  });

  // Pagination
  const activeCount = panels[_lcActiveTab]?.rows.length || 0;
  const totalPages  = Math.ceil(activeCount / _lcPageSize) || 1;
  const pag = document.getElementById('lc-pagination');
  if(pag){
    pag.innerHTML =
      `<span style="font-size:12.5px;color:var(--sub);">${activeCount.toLocaleString()} registros · Pág ${Math.min(_lcPage,totalPages)} / ${totalPages}</span>
       <div style="display:flex;gap:6px;">
         <button class="btn btn-ghost" onclick="_lcPage=Math.max(1,_lcPage-1);renderLCTable()" ${_lcPage<=1?'disabled':''}>← Anterior</button>
         <button class="btn btn-ghost" onclick="_lcPage=Math.min(${totalPages},_lcPage+1);renderLCTable()" ${_lcPage>=totalPages?'disabled':''}>Siguiente →</button>
       </div>`;
  }
}

function initLifecycle(){
  renderLCTable();
}

function processAll(){
  if(!window.DATASET) return;
  const pending = DATASET.backlog.filter(o=>o.subStatus==='pending'||!o.subStatus);
  if(!pending.length){ showToast('✅ No hay pedidos pendientes en cola'); return; }
  showToast(`⚡ Procesando ${pending.length} pedidos en lote…`);
  let i=0;
  const interval = setInterval(()=>{
    if(i>=pending.length){ clearInterval(interval); showToast(`✅ ${pending.length} órdenes enviadas a SAP SD`); renderLCTable(); return; }
    processOrder(pending[i].sapNum);
    i++;
  }, 120);
}

function renderBacklogTable(){ renderLCTable(); }


// ── SAP Population ──
function populateSap(orderId){
  const o = orders[orderId];
  if(!o) return;

  // VA01 header
  const t = document.getElementById('va01-win-title');
  if(t) t.textContent = 'Display Sales Order: Overview — ' + o.sapNum;

  ['va01-sapnum','va01-uuid','va01-soldto-name','va01-pono','va01-orderdate','va01-delivdate',
   'va01-netval','va01-delivnum','va01-gidate','va01-weight'].forEach(id => {
    const el = document.getElementById(id);
    const key = id.replace('va01-','').replace(/-([a-z])/g, (_,c)=>c.toUpperCase());
    const map = {
      sapnum:'sapNum', uuid:'uuid', soldtoname:'soldToName', pono:'poNumber',
      orderdate:'orderDate', delivdate:'delivDate', netval:'netVal',
      delivnum:'delivNum', gidate:'giDate', weight:'weight'
    };
    if(el && o[map[id.replace('va01-','')] || key]) el.textContent = o[map[id.replace('va01-','')]||key] || '—';
  });

  // VA01 items table
  const va01Body = document.querySelector('#view-sap-va01 tbody');
  if(va01Body && o.items){
    va01Body.innerHTML = o.items.map(it =>
      `<tr><td>${it.pos}</td><td>${it.sku}</td><td>${it.desc}</td>
       <td>${it.qty}</td><td>${it.unit}</td><td>${it.price}</td>
       <td>${it.plant}</td><td>${it.delivDate}</td>
       <td><span style="background:${it.status==='Completed'?'#DCFCE7':'#FEF9C3'};color:${it.status==='Completed'?'#15803D':'#854D0E'};border-radius:10px;padding:2px 8px;font-size:11px;">${it.status}</span></td>
      </tr>`
    ).join('');
  }

  // VL01N
  const vl01Body = document.getElementById('vl01n-tbody');
  if(vl01Body && o.delivItems){
    vl01Body.innerHTML = o.delivItems.map(it =>
      `<tr><td>${it.pos}</td><td>${it.sku}</td><td>${it.desc}</td>
       <td>${it.qty}</td><td>${it.unit}</td><td>${it.pickQty}</td>
       <td>${it.sloc}</td><td>${it.batch}</td></tr>`
    ).join('');
  }

  // VL02N
  const vl02Body = document.getElementById('vl02n-tbody');
  if(vl02Body && o.delivItems){
    vl02Body.innerHTML = o.delivItems.map(it =>
      `<tr><td>${it.pos}</td><td>${it.sku}</td><td>${it.desc}</td>
       <td>${it.qty}</td><td>${it.unit}</td><td>${it.pickQty}</td>
       <td>${it.sloc}</td><td>${it.batch}</td></tr>`
    ).join('');
  }

  // Fill common VL fields
  const vl1Fields = {
    'vl01n-deliv-num':o.delivNum,'vl01n-so-ref':o.sapNum,
    'vl01n-shipto-name':o.soldToName,'vl01n-gidate':o.giDate
  };
  Object.entries(vl1Fields).forEach(([id,val]) => {
    const el = document.getElementById(id);
    if(el) el.textContent = val||'—';
  });
  const vl2Fields = {
    'vl02n-deliv-num':o.delivNum,'vl02n-shipto-name':o.soldToName,'vl02n-gi-date':o.giDate
  };
  Object.entries(vl2Fields).forEach(([id,val]) => {
    const el = document.getElementById(id);
    if(el) el.textContent = val||'—';
  });
}

// ── Processing actions ──
function processAll(){
  showToast('⚡ Procesando ' + DATASET.backlog.length + ' órdenes en cola…');
  setTimeout(() => showToast('✅ ' + DATASET.backlog.length + ' órdenes enviadas a SAP SD'), 2200);
}

function processFromDetail(){
  closeModal('modal-detail');
  showToast('⚡ Procesando orden en SAP SD…');
  setTimeout(() => showToast('✅ Sales Order creada en SAP'), 1500);
}

function postGI(){
  showToast('📦 Registrando Goods Issue en VL02N…');
  setTimeout(() => {
    const st = document.getElementById('vl02n-gi-st');
    const st2 = document.getElementById('vl02n-gi-st2');
    if(st)  st.textContent  = 'C — GI posted';
    if(st2) st2.textContent = 'C — GI posted';
    const icon = document.getElementById('vl02n-st-icon');
    if(icon) { icon.textContent='✓'; icon.style.color='#22C55E'; }
    showToast('✅ Goods Issue registrado exitosamente');
  }, 1800);
}

function syncEmail(){
  showToast('🔄 Sincronizando bandeja de entrada…');
  setTimeout(() => showToast('✅ 9 correos — Bandeja actualizada'), 1400);
}

// ── Business Rules actions ──
function addNewRule(){
  showToast('➕ Abriendo formulario de nueva regla…');
}

function applyFix(){
  closeModal('modal-error');
  showToast('🔧 Aplicando corrección automática…');
  setTimeout(() => {
    showToast('✅ Corrección aplicada — Reintentando SAP');
  }, 1600);
}

function confirmFix(){
  closeModal('modal-fix');
  showToast('✅ Corrección confirmada');
}

// ── Agent logs ──
function openLogs(agentId){
  const ag = agentsData.find(a => a.id === agentId);
  const title = document.getElementById('logs-modal-title');
  const body  = document.getElementById('logs-modal-body');
  if(title) title.textContent = (ag ? ag.name : agentId) + ' — Execution Log';
  const entries = [
    {t:'14:47:02',type:'ok', msg:'Agent cycle started'},
    {t:'14:47:03',type:'ok', msg:'RFC connection established: CAF1 (200ms)'},
    {t:'14:47:04',type:'ok', msg:'Queue fetched: 3 items pending'},
    {t:'14:47:05',type:'ok', msg:'Processing item 1/3 — 76933175'},
    {t:'14:47:07',type:'ok', msg:'BAPI_SALESORDER_CREATEFROMDAT2 → 200ms → SO 100025255'},
    {t:'14:47:08',type:'ok', msg:'Processing item 2/3 — 76933070'},
    {t:'14:47:10',type:'ok', msg:'BAPI_SALESORDER_CREATEFROMDAT2 → 185ms → SO 100025256'},
    {t:'14:47:11',type:'warn',msg:'Processing item 3/3 — 76933065'},
    {t:'14:47:12',type:'err', msg:'BAPI error: Material PKG-602 not found in plant CAF1'},
    {t:'14:47:12',type:'err', msg:'Order 76933065 blocked — manual intervention required'},
    {t:'14:47:13',type:'ok', msg:'Cycle completed: 2 success, 1 error'},
    {t:'14:47:14',type:'ok', msg:'Heartbeat sent — Agent alive'}
  ];
  if(body){
    const colors = {ok:'#22C55E', warn:'#F59E0B', err:'#EF4444'};
    body.innerHTML = '<div style="font-family:monospace;font-size:12px;line-height:1.9;">' +
      entries.map(e =>
        `<div><span style="color:#94a3b8;">[${e.t}]</span> <span style="color:${colors[e.type]||'#ccc'};font-weight:700;">[${e.type.toUpperCase()}]</span> ${e.msg}</div>`
      ).join('') +
      '</div>';
  }
  openModal('modal-logs');
}

// ── Override renderEmails to handle new emailsData schema ──
function renderEmails(){
  const el = document.getElementById('email-list-body');
  if(!el) return;
  el.innerHTML = emailsData.map(e => {
    const isUnread = e.unread === true || e.read === false;
    const isActive = activeEmailId === e.id;
    return `<div class="email-item ${isUnread?'unread':''} ${isActive?'active':''}" onclick="openEmail('${e.id}')" id="eitem-${e.id}">
      ${isUnread?'<span class="unread-dot"></span>':''}
      <div class="email-item-from"><span>${e.fromName||e.from||'—'}</span><span class="email-item-time">${e.time||''}</span></div>
      <div class="email-item-subject">${e.subject||'(sin asunto)'}</div>
      <div class="email-item-preview">${e.preview||''}</div>
    </div>`;
  }).join('');
}

// ── Init ──
document.querySelectorAll('.modal-overlay').forEach(o => {
  o.addEventListener('click', e => { if(e.target === o) o.classList.remove('open'); });
});
initLifecycle();
populateSap('s001');
renderEmails();

// ════════════════════════════════════════════════════════════
//  EMAIL: OTC Stepper helpers
// ════════════════════════════════════════════════════════════
function _getOTCStep(email){
  if(email.tag==='error')   return 2;
  if(email.tag==='urgente') return 2;
  if(email.tag==='oc')      return email.read ? 3 : 2;
  if(email.tag==='resumen') return 5;
  return 2;
}
function _buildOTCStepperHtml(cur){
  const steps=[
    {n:1,label:'Email\nRecibido'},
    {n:2,label:'Parseo IA'},
    {n:3,label:'Validación\nSAP'},
    {n:4,label:'PV Creado'},
    {n:5,label:'Entrega SAP'},
    {n:6,label:'Cierre OTC'}
  ];
  return '<div class="otc-stepper">'+steps.map(s=>{
    const done=s.n<cur,act=s.n===cur;
    const cls=done?'done':act?'active':'';
    const inner=done?'<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="3"><polyline points="20 6 9 17 4 12"/></svg>'
      :act?'<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2.5"><path d="M21.5 2v6h-6M2.5 22v-6h6M2 11.5a10 10 0 0 1 18.8-4.3M22 12.5a10 10 0 0 1-18.8 4.2"/></svg>'
      :'<span style="font-size:13px;">'+s.n+'</span>';
    return '<div class="otc-step '+cls+'"><div class="otc-step-circle">'+inner+'</div><div class="otc-step-label">'+s.label.replace('\n','<br>')+'</div></div>';
  }).join('')+'</div>';
}

// ── Override openEmail with OTC stepper ──────────────────────
function openEmail(id){
  activeEmailId=id;
  const email=emailsData.find(e=>e.id===id);
  if(!email) return;
  email.read=true; email.unread=false; renderEmails();
  const panel=document.getElementById('email-panel')||document.getElementById('email-detail-content');
  if(!panel) return;
  const isOraclePO=['oc','urgente'].includes(email.tag);
  const isError=email.tag==='error';
  const cur=_getOTCStep(email);
  const ocNum=email.poNumber||email.oraclePOId||'';
  const ocBadge=ocNum?`<span class="email-oc-badge">${ocNum}</span>`:'';
  const tagBadge=isOraclePO
    ?'<span style="display:flex;align-items:center;gap:5px;background:#FFF5F5;border:1px solid #FCA5A5;padding:3px 10px;border-radius:8px;"><span style="color:#CC0000;font-weight:900;font-size:12px;">ORACLE</span><span style="color:#555;font-size:11px;"> Retail</span></span>'
    :isError?'<span style="background:#FFF1F0;border:1px solid #FCA5A5;padding:3px 10px;border-radius:8px;font-size:11px;font-weight:700;color:#CC0000;">⚠ ERROR SAP</span>':'';
  let bodyHtml;
  if(email.body&&email.body.trim().startsWith('<')){bodyHtml=email.body;}
  else{const raw=email.body||mkEmailBody(email.area||'');bodyHtml='<pre style="font-family:\'Courier New\',monospace;font-size:13px;white-space:pre-wrap;line-height:1.9;color:#222;margin:0;">'+raw+'</pre>';}
  let attHtml='';
  if(email.attachments&&email.attachments.length){
    const icons={pdf:'<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#CC0000" stroke-width="2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14,2 14,8 20,8"/></svg>',xlsx:'<svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#217346" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2"/><line x1="3" y1="9" x2="21" y2="9"/><line x1="3" y1="15" x2="21" y2="15"/><line x1="9" y1="3" x2="9" y2="21"/></svg>'};
    attHtml='<div style="border-top:1px solid var(--border);padding:12px 20px;background:var(--light);display:flex;gap:10px;flex-wrap:wrap;">';
    email.attachments.forEach(att=>{
      const ic=icons[att.type]||icons.pdf;
      const pk=att.poRef||att.poId;
      const fn=pk&&ORACLE_PO_DATA[pk]?`openOraclePOViewer('${pk}')`:att.type==='xlsx'?'openExcelSummaryViewer()':(`showToast('📎 ${att.name}')`);
      attHtml+=`<div onclick="${fn}" style="display:flex;align-items:center;gap:8px;padding:8px 14px;background:white;border:1.5px solid var(--border);border-radius:10px;cursor:pointer;font-size:12.5px;" onmouseover="this.style.borderColor='var(--orange)'" onmouseout="this.style.borderColor='var(--border)'">${ic}<div><div style="font-weight:600;color:var(--text);">${att.name}</div><div style="font-size:10.5px;color:var(--sub);">${att.size}</div></div></div>`;
    });
    attHtml+='</div>';
  }
  panel.innerHTML=
    `<div style="padding:16px 20px 12px;background:white;border-bottom:1px solid var(--border);">
      <div style="font-size:16px;font-weight:800;color:var(--text);margin-bottom:8px;line-height:1.3;">${email.subject}</div>
      <div class="email-meta-row">
        <b style="color:var(--text);">De: ${email.fromName||email.from}</b>
        <span>&lt;${email.fromEmail||email.from||'rommel.gil.vera@emeal.nttdata.com'}&gt;</span>
        <span>·</span><span><b>Para:</b> ${email.to||'pedidos@caffenio.com'}</span>
        <span>·</span><span><b>Hora:</b> ${email.time||'—'}</span>
        <span style="margin-left:4px;">${ocBadge}</span>
        ${tagBadge?'<span style="margin-left:auto;">'+tagBadge+'</span>':''}
      </div>
    </div>
    <div style="flex:1;overflow-y:auto;background:white;">
      <div class="email-section-lbl"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="var(--orange)" stroke-width="2.5"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>FLUJO DE PROCESAMIENTO OTC</div>
      ${_buildOTCStepperHtml(cur)}
      <div class="email-section-lbl" style="border-top:1px solid var(--border);"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="var(--sub)" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>CONTENIDO DEL CORREO</div>
      <div style="padding:14px 20px 20px;">${bodyHtml}</div>
    </div>
    ${attHtml}
    <div style="padding:10px 20px;border-top:1px solid var(--border);display:flex;gap:8px;background:var(--light);">
      <button class="btn btn-orange" onclick="showToast('↩ Respuesta enviada')">↩ Responder</button>
      <button class="btn btn-ghost" onclick="showToast('✉ Reenviado')">→ Reenviar</button>
      ${isOraclePO?'<button class="btn btn-dark" onclick="showToast(\'⚡ Procesando en SAP SD…\')"><svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="5 3 19 12 5 21 5 3"/></svg> Procesar en SAP</button>':''}
    </div>`;
}

// ════════════════════════════════════════════════════════════
//  LIFECYCLE: Detail modal
// ════════════════════════════════════════════════════════════
function openOrderDetail(sapNum){
  const o=DATASET?DATASET.all.find(x=>x.sapNum===sapNum):null;
  if(!o){showToast('Orden no encontrada');return;}
  const store=OXXO_STORES.find(s=>s.name===o.fromName)||{};
  const uuid=o.sapNum.slice(-8);
  const dp=o.date.split('/');
  const ord=new Date(+dp[2],+dp[1]-1,+dp[0]); ord.setDate(ord.getDate()+2);
  const delDate=`${String(ord.getDate()).padStart(2,'0')}/${String(ord.getMonth()+1).padStart(2,'0')}/${ord.getFullYear()}`;
  const fmt=n=>'$'+n.toLocaleString('es-MX',{minimumFractionDigits:2,maximumFractionDigits:2});
  const isWarn=o.subStatus==='warn';
  const checks=[
    {ok:!isWarn&&o.errorCode!=='CUST-MAP-001',label:'Cliente en KNA1',sub:`KUNNR: ${o.areaShort}`},
    {ok:o.errorCode!=='MAT-SKU-404',label:'Material en MARA',sub:`SKU: ${o.items[0]?o.items[0].sku:'—'}`},
    {ok:o.errorCode!=='STO-CHK-003',label:'Stock disponible (MMBE)',sub:`${o.items[0]?o.items[0].qty:0} ${o.items[0]?o.items[0].desc.split(' ').pop():'uds'} solicitados`},
    {ok:o.errorCode!=='PRC-COND-002',label:'Condición de precio (KONP)',sub:'Lista de precios vigente'},
    {ok:true,label:'Límite de cantidad',sub:'Sin restricciones'}
  ];
  document.getElementById('detail-modal-title').textContent='📋 Detalle — '+o.fromName;
  document.getElementById('detail-modal-sub').textContent=`OC recibida ${o.date}, ${o.recvTime||'09:00'} · ${o.status==='backlog'?'Pendiente de procesamiento':o.status==='success'?'Procesado':'Error'}`;
  window._detailSapNum=sapNum;
  document.getElementById('detail-modal-body').innerHTML=`
    <div style="padding:0 24px 4px;">
      <div style="font-size:11.5px;font-weight:800;color:var(--sub);letter-spacing:.7px;text-transform:uppercase;padding:16px 0 10px;display:flex;align-items:center;gap:7px;">📦 Información del Pedido</div>
      <div class="det-grid">
        <div class="det-cell"><div class="det-lbl">Cliente / Área</div><div class="det-val">${o.fromName}</div></div>
        <div class="det-cell"><div class="det-lbl">Fecha / Hora</div><div class="det-val">${o.date.split('/').reverse().join('/')}, ${o.recvTime||'09:00'}</div></div>
        <div class="det-cell"><div class="det-lbl">Nº OC / PO</div><div class="det-val mono">${o.poNumber}</div></div>
        <div class="det-cell"><div class="det-lbl">UUID</div><div class="det-val mono">${uuid}</div></div>
        <div class="det-cell"><div class="det-lbl">SKU Principal</div><div class="det-val blue" onclick="showToast('SKU: ${o.items[0]?o.items[0].sku:''}')">${o.items[0]?o.items[0].sku:'—'}</div></div>
        <div class="det-cell"><div class="det-lbl">Total Pedido</div><div class="det-val big">${fmt(o.totalMXN)} MXN</div></div>
        <div class="det-cell"><div class="det-lbl">Dirección Entrega</div><div class="det-val" style="font-size:12.5px;">${store.addr||o.storeCity}</div></div>
        <div class="det-cell"><div class="det-lbl">Fecha Solicitada</div><div class="det-val">${delDate}</div></div>
      </div>
    </div>
    <div style="padding:0 24px 4px;">
      <div style="font-size:11.5px;font-weight:800;color:var(--sub);letter-spacing:.7px;text-transform:uppercase;padding:16px 0 10px;">📋 Líneas del Pedido</div>
      <div style="border:1px solid var(--border);border-radius:12px;overflow:hidden;">
        <table class="det-items-tbl">
          <thead><tr><th style="width:48px;">#</th><th>SKU</th><th>Descripción</th><th style="text-align:right;">Cant.</th><th style="text-align:right;">P.Unit.</th><th style="text-align:right;">Importe</th></tr></thead>
          <tbody>${o.items.map((it,i)=>`<tr>
            <td style="color:var(--sub);font-size:11px;">${String(i+1).padStart(3,'0')}</td>
            <td class="sku" onclick="showToast('SKU: ${it.sku}')">${it.sku}</td>
            <td>${it.desc}</td>
            <td class="qty" style="text-align:right;">${it.qty} ${it.desc.split(' ').pop()}</td>
            <td style="text-align:right;color:var(--sub);">$${(it.price||0).toFixed(2)}</td>
            <td class="tot" style="text-align:right;">${fmt(it.total)}</td>
          </tr>`).join('')}</tbody>
        </table>
        <div style="padding:10px 16px;background:#F8FAFC;border-top:2px solid var(--border);display:flex;justify-content:flex-end;gap:20px;font-size:13px;">
          <span style="color:var(--sub);">Líneas: <b>${o.items.length}</b></span>
          <span style="font-weight:800;color:var(--orange);font-size:15px;">${fmt(o.totalMXN)} MXN</span>
        </div>
      </div>
    </div>
    <div style="padding:0 24px 24px;">
      <div style="font-size:11.5px;font-weight:800;color:var(--sub);letter-spacing:.7px;text-transform:uppercase;padding:16px 0 10px;">⚙ Validación SAP SD</div>
      ${checks.map(c=>`<div class="sap-chk${c.ok?'':' fail'}">
        <div class="sap-chk-ico ${c.ok?'ok':'fail'}">${c.ok?'✓':'✗'}</div>
        <div><div style="font-size:13px;font-weight:700;color:${c.ok?'#15803D':'#DC2626'};">${c.label}</div><div style="font-size:11.5px;color:var(--sub);">${c.sub}</div></div>
      </div>`).join('')}
    </div>`;
  openModal('modal-detail');
}

function processFromDetail(){
  const sapNum=window._detailSapNum;
  closeModal('modal-detail');
  if(sapNum) processOrder(sapNum);
  else{showToast('⚡ Procesando…');setTimeout(()=>showToast('✅ Sales Order creada en SAP'),1500);}
}

// ════════════════════════════════════════════════════════════
//  WARN MODAL redesign
// ════════════════════════════════════════════════════════════
const WARN_CATALOG={
  'STO-CHK-003':{title:'Sin stock disponible',msg:o=>`Stock insuficiente en planta CAF1 para <b>${o.items[0]?o.items[0].sku:'SKU'}</b>. Cantidad solicitada: <b>${o.items[0]?o.items[0].qty:0} ${o.items[0]?o.items[0].desc.split(' ').pop():'uds'}</b>. Se requiere ajuste o reabasto.`,
    opts:[{label:'Ajuste automático de cantidad',desc:'El agente ajusta al stock disponible en MMBE y crea el PV con cantidad corregida.'},{label:'Diferir — Esperar reabasto',desc:'La orden queda en espera hasta disponibilidad. Notificación automática al completarse.'}]},
  'PRC-COND-002':{title:'Condición de precio no encontrada',msg:o=>`No existe condición de precio vigente (KONP) para <b>${o.poNumber}</b>. Total: <b>$${(o.totalMXN||0).toLocaleString('es-MX')} MXN</b>.`,
    opts:[{label:'Escalar a Gestión de Precios',desc:'Solicitar actualización a Controlling. Tiempo estimado: 2-4 hrs.'},{label:'Aplicar precio base de catálogo',desc:'El agente usa el precio más reciente y genera aviso a Controlling para validación posterior.'}]},
  'CUST-MAP-001':{title:'Cliente no verificado en KNA1',msg:o=>`Remitente <b>${o.fromName}</b> no está en la whitelist de clientes habilitados. KUNNR no determinado automáticamente.`,
    opts:[{label:'Mapeo automático por fuzzy-match',desc:'Busca cliente más similar en KNA1 (confianza 89%).'},{label:'Escalar a Administración de Clientes',desc:'Abrir ticket para verificar y registrar en KNA1. Tiempo: 4-8 hrs.'}]},
  'MAT-SKU-404':{title:'Material no encontrado en MARA',msg:o=>`SKU <b>${o.items[0]?o.items[0].sku:'—'}</b> no existe en el maestro de materiales de planta <b>CAF1</b>. Posible material descontinuado o no creado.`,
    opts:[{label:'Fuzzy-match de SKU alternativo',desc:'Busca el material más similar en MARA por nombre/características. Confianza: 87%.'},{label:'Solicitar creación MM01',desc:'Abrir solicitud urgente al equipo de Materiales. Tiempo estimado: 2-4 hrs.'}]},
  'default':{title:'Cantidad supera límite por SKU',msg:o=>`Cantidad <b>${o.items[0]?o.items[0].qty+' '+o.items[0].desc.split(' ').pop():'—'}</b> supera el máximo por SKU. Sugerencia: dividir en 2 órdenes o ajustar.`,
    opts:[{label:'Procesar con ajuste automático',desc:'El agente aplica la corrección y crea el PV con cantidad ajustada.'},{label:'Escalar a revisión manual',desc:'Asignar al jefe de compras para validación antes del PV.'}]}
};

function openWarnModal(sapNum){
  _warnTargetId=sapNum; _warnSelected=null;
  const o=DATASET?DATASET.all.find(x=>x.sapNum===sapNum):null;
  if(!o){showToast('Orden no encontrada');return;}
  const cat=WARN_CATALOG[o.errorCode||'default']||WARN_CATALOG['default'];
  const titleEl=document.getElementById('warn-modal-title-txt');
  const subEl=document.getElementById('warn-modal-sub');
  const alertEl=document.getElementById('warn-alert-area');
  const contEl=document.getElementById('warn-options-container');
  const btn=document.getElementById('warn-apply-btn');
  if(titleEl) titleEl.textContent='Advertencia — '+o.fromName;
  if(subEl)   subEl.textContent='Diagnóstico Agente IA';
  if(alertEl) alertEl.innerHTML=`<div class="warn-alert"><div class="warn-alert-ttl"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"/></svg>Advertencia detectada por Agente IA</div><div class="warn-alert-body">${cat.msg(o)}</div></div>`;
  if(contEl) contEl.innerHTML=cat.opts.map((opt,i)=>`<div class="warn-ropt" id="wropt-${i}" onclick="selectWarnOpt(${i})"><div class="warn-radio" id="wropt-dot-${i}"><div class="warn-radio-dot"></div></div><div><div class="warn-rlbl">${opt.label}</div><div class="warn-rdesc">${opt.desc}</div></div></div>`).join('');
  if(btn){btn.disabled=true;btn.style.opacity='.5';}
  openModal('modal-warn-correction');
}

function selectWarnOpt(idx){
  _warnSelected='w'+(idx+1);
  document.querySelectorAll('.warn-ropt').forEach((el,i)=>el.classList.toggle('sel',i===idx));
  const btn=document.getElementById('warn-apply-btn');
  if(btn){btn.disabled=false;btn.style.opacity='1';}
}

function applyWarnCorrection(){
  if(!_warnTargetId||!_warnSelected) return;
  closeModal('modal-warn-correction');
  const o=DATASET?DATASET.all.find(x=>x.sapNum===_warnTargetId):null;
  if(!o) return;
  if(_warnSelected==='w1'){showToast('🤖 Agente aplicando corrección automática…');setTimeout(()=>processOrder(_warnTargetId),900);}
  else{showToast('👤 Escalando a revisión manual — Ticket generado');o.subStatus='deferred';renderLCTable();}
  _warnTargetId=null; _warnSelected=null;
}

// ════════════════════════════════════════════════════════════
//  LIFECYCLE: renderLCTable + processAll + initLifecycle
// ════════════════════════════════════════════════════════════
function renderLCTable(){
  if(!window.DATASET) return;
  const base=_lcApplyFilters(DATASET.all);
  const total=base.length;
  const success=base.filter(o=>o.status==='success').length;
  const backlog=base.filter(o=>o.status==='backlog').length;
  const errors=base.filter(o=>o.status==='error').length;
  const setEl=(id,v)=>{const e=document.getElementById(id);if(e)e.textContent=v;};
  setEl('cnt-all',total.toLocaleString()); setEl('cnt-success',success.toLocaleString());
  setEl('cnt-backlog',backlog.toLocaleString()); setEl('cnt-errors',errors.toLocaleString());
  setEl('tc-backlog',backlog); setEl('tc-success',success); setEl('tc-errors',errors);
  const pc=document.getElementById('lc-pill-count'); if(pc) pc.textContent=total.toLocaleString();
  const fmt=n=>n.toLocaleString('es-MX',{minimumFractionDigits:0,maximumFractionDigits:0});
  const mkSummary=items=>{
    if(!items||!items.length) return '—';
    const names=items.slice(0,3).map(it=>it.desc.toUpperCase().split(' ').slice(0,2).join(' ')).join(' + ');
    const tot=items.reduce((s,it)=>s+it.total,0);
    return `<div style="font-size:12.5px;font-weight:600;color:var(--text);line-height:1.4;">${names.length>42?names.substring(0,42)+'…':names}</div><div style="font-size:11px;color:var(--sub);margin-top:2px;">${items.length} SKU${items.length>1?'s':''} / <b style="color:var(--text);">$${fmt(tot)} MXN</b></div>`;
  };
  const panels={
    backlog:{rows:base.filter(o=>o.status==='backlog'),el:'backlog-rows',rowFn:o=>{
      const isW=o.subStatus==='warn'||o.subStatus==='deferred';
      const badge=isW?'<span class="lc-badge lc-badge-warn"><svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"/></svg>WARN</span>':'<span class="lc-badge lc-badge-pending"><svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>PENDING</span>';
      const act=isW?`<button class="btn-warn" onclick="openWarnModal('${o.sapNum}')"><svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"/></svg>Advertencia</button>`:`<button class="btn-sap" onclick="processOrder('${o.sapNum}')"><svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><polyline points="5 12 12 5 19 12"/><polyline points="5 19 12 12 19 19"/></svg>→SAP</button>`;
      return `<div class="table-row grid-backlog"><span><input type="checkbox" class="lc-check"></span><span><div style="font-weight:700;font-size:13px;color:var(--text);">${o.fromName}</div><div style="font-size:10.5px;font-family:var(--mono);color:var(--sub);margin-top:2px;">${o.poNumber}</div></span><span><div style="font-size:12.5px;">${o.date.split('/').reverse().join('/')}</div><div style="font-size:11px;color:var(--sub);">${o.recvTime||'09:00'}</div></span><span>${mkSummary(o.items)}</span><span>${badge}</span><span style="display:flex;gap:6px;align-items:center;flex-wrap:wrap;"><button class="btn-detail" onclick="openOrderDetail('${o.sapNum}')">Detalle</button>${act}<button class="btn-kebab" onclick="showToast('⋮')">⋮</button></span></div>`;
    }},
    success:{rows:base.filter(o=>o.status==='success'),el:'success-rows',rowFn:o=>`<div class="table-row grid-success"><span><input type="checkbox" class="lc-check"></span><span><div style="font-weight:700;font-size:13px;color:var(--text);">${o.fromName}</div><div style="font-size:10.5px;font-family:var(--mono);color:var(--sub);margin-top:2px;">${o.poNumber}</div></span><span><div style="font-size:12.5px;">${o.date.split('/').reverse().join('/')}</div><div style="font-size:11px;color:var(--sub);">${o.recvTime||'—'}</div></span><span>${mkSummary(o.items)}</span><span><span class="lc-badge lc-badge-success">✓ Procesado</span></span><span style="font-family:var(--mono);font-size:12px;font-weight:700;color:#16A34A;">${o.soNumber||'—'}</span><span style="display:flex;gap:6px;align-items:center;"><button class="btn-detail" onclick="openOrderDetail('${o.sapNum}')">Detalle</button><span style="font-size:11px;color:var(--sub);">${o.processingTime}min</span></span></div>`},
    errors:{rows:base.filter(o=>o.status==='error'),el:'errors-rows',rowFn:o=>`<div class="table-row grid-errors"><span><input type="checkbox" class="lc-check"></span><span><div style="font-weight:700;font-size:13px;color:var(--text);">${o.fromName}</div><div style="font-size:10.5px;font-family:var(--mono);color:var(--sub);margin-top:2px;">${o.poNumber}</div></span><span><div style="font-size:12.5px;">${o.date.split('/').reverse().join('/')}</div><div style="font-size:11px;color:var(--sub);">${o.recvTime||'—'}</div></span><span style="font-size:12.5px;">${o.sku||'—'}</span><span><span class="lc-badge lc-badge-error">✗ Error</span><div style="font-size:10.5px;font-family:var(--mono);color:#DC2626;margin-top:4px;">${o.errorCode||'—'}</div></span><span style="font-family:var(--mono);font-size:11px;">—</span><span style="display:flex;gap:6px;align-items:center;flex-wrap:wrap;"><button class="btn-detail" onclick="openOrderDetail('${o.sapNum}')">Detalle</button><button class="btn-warn" onclick="openWarnModal('${o.sapNum}')">Fix</button></span></div>`}
  };
  Object.entries(panels).forEach(([tab,cfg])=>{
    const el=document.getElementById(cfg.el); if(!el) return;
    const totalR=cfg.rows.length,totalP=Math.ceil(totalR/_lcPageSize)||1,pg=Math.min(_lcPage,totalP);
    el.innerHTML=cfg.rows.slice((pg-1)*_lcPageSize,pg*_lcPageSize).map(cfg.rowFn).join('')||'<div style="padding:48px;text-align:center;color:var(--sub);"><div style="font-size:32px;margin-bottom:8px;">🎉</div><div style="font-weight:600;">Sin registros</div></div>';
  });
  const ac=panels[_lcActiveTab]?.rows.length||0,tp=Math.ceil(ac/_lcPageSize)||1;
  const pag=document.getElementById('lc-pagination');
  if(pag) pag.innerHTML=`<span style="font-size:12.5px;color:var(--sub);">${ac.toLocaleString()} registros · Pág ${Math.min(_lcPage,tp)} / ${tp}</span><div style="display:flex;gap:6px;"><button class="btn btn-ghost" onclick="_lcPage=Math.max(1,_lcPage-1);renderLCTable()" ${_lcPage<=1?'disabled':''}>← Anterior</button><button class="btn btn-ghost" onclick="_lcPage=Math.min(${tp},_lcPage+1);renderLCTable()" ${_lcPage>=tp?'disabled':''}>Siguiente →</button></div>`;
}

function initLifecycle(){ renderLCTable(); }
function processAll(){
  if(!window.DATASET) return;
  const pending=DATASET.backlog.filter(o=>!o.subStatus||o.subStatus==='pending');
  if(!pending.length){showToast('✅ Sin pedidos pendientes');return;}
  showToast(`⚡ Procesando ${pending.length} pedidos en lote…`);
  let i=0; const iv=setInterval(()=>{if(i>=pending.length){clearInterval(iv);showToast(`✅ ${pending.length} órdenes enviadas a SAP SD`);renderLCTable();return;}processOrder(pending[i].sapNum);i++;},120);
}
function renderBacklogTable(){renderLCTable();}

// ── Re-init ──
document.querySelectorAll('.modal-overlay').forEach(o=>{o.addEventListener('click',e=>{if(e.target===o)o.classList.remove('open');});});
initLifecycle();
populateSap('s001');
renderEmails();

</script>
</body>
</html>
