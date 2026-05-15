<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="DXDupes - a clean dupe log website for GitHub Pages." />
  <title>DXDupes</title>
  <style>
    :root{
      --bg:#070914;
      --bg2:#0d1020;
      --card:#11162a;
      --card2:#161c35;
      --text:#eef1ff;
      --muted:#a5add0;
      --line:rgba(255,255,255,.08);
      --purple:#9b5cff;
      --purple2:#6a2bff;
      --blue:#3b82f6;
      --green:#29d39c;
      --red:#ff5f7a;
      --shadow:0 20px 60px rgba(0,0,0,.35);
      --radius:24px;
    }

    *{box-sizing:border-box}
    html{scroll-behavior:smooth}
    body{
      margin:0;
      font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background:
        radial-gradient(circle at top left, rgba(155,92,255,.25), transparent 28%),
        radial-gradient(circle at top right, rgba(59,130,246,.20), transparent 28%),
        linear-gradient(180deg, var(--bg), var(--bg2));
      color:var(--text);
      min-height:100vh;
    }

    a{color:inherit;text-decoration:none}
    button,input,select,textarea{font:inherit}

    .wrap{max-width:1180px;margin:0 auto;padding:20px}
    .nav{
      display:flex;align-items:center;justify-content:space-between;gap:16px;
      padding:14px 18px;border:1px solid var(--line);background:rgba(15,18,36,.78);
      backdrop-filter: blur(16px); border-radius:999px; position:sticky; top:14px; z-index:20; box-shadow:var(--shadow);
    }
    .brand{display:flex;align-items:center;gap:12px;font-weight:800;letter-spacing:.4px}
    .logo{
      width:38px;height:38px;border-radius:14px;display:grid;place-items:center;
      background:linear-gradient(135deg,var(--purple),var(--blue));
      box-shadow:0 10px 30px rgba(123,92,255,.35);
      font-weight:900;
    }
    .navlinks{display:flex;gap:14px;flex-wrap:wrap;justify-content:flex-end}
    .navlinks a{color:var(--muted);padding:10px 12px;border-radius:999px;transition:.2s}
    .navlinks a:hover{background:rgba(255,255,255,.06);color:var(--text)}

    .hero{
      display:grid;grid-template-columns:1.3fr .9fr;gap:22px;align-items:stretch;
      margin:28px 0 20px;
    }
    .panel{
      background:linear-gradient(180deg, rgba(17,22,42,.92), rgba(12,15,29,.92));
      border:1px solid var(--line);
      border-radius:var(--radius);
      box-shadow:var(--shadow);
      overflow:hidden;
    }
    .hero-main{padding:34px}
    .eyebrow{
      display:inline-flex;align-items:center;gap:8px;
      padding:8px 12px;border:1px solid rgba(155,92,255,.35);
      background:rgba(155,92,255,.12);border-radius:999px;color:#d9c9ff;font-size:13px;
    }
    h1{margin:16px 0 12px;font-size:clamp(2.4rem,5vw,4.8rem);line-height:1.02}
    .grad{background:linear-gradient(90deg,#fff,var(--purple),var(--blue));-webkit-background-clip:text;background-clip:text;color:transparent}
    .sub{color:var(--muted);font-size:1.03rem;line-height:1.7;max-width:62ch}
    .actions{display:flex;gap:12px;flex-wrap:wrap;margin-top:22px}
    .btn{
      border:none;cursor:pointer;border-radius:16px;padding:14px 18px;font-weight:700;
      transition:.18s;display:inline-flex;align-items:center;justify-content:center;gap:10px;
    }
    .btn-primary{background:linear-gradient(135deg,var(--purple),var(--blue));color:white;box-shadow:0 14px 40px rgba(90,102,255,.26)}
    .btn-primary:hover{transform:translateY(-1px)}
    .btn-ghost{background:rgba(255,255,255,.05);color:var(--text);border:1px solid var(--line)}
    .btn-ghost:hover,.navlinks a:hover{transform:translateY(-1px)}

    .hero-side{display:grid;gap:14px;padding:18px}
    .statgrid{display:grid;grid-template-columns:repeat(2,1fr);gap:12px}
    .stat{
      padding:18px;border-radius:22px;background:rgba(255,255,255,.04);border:1px solid var(--line)
    }
    .stat .n{font-size:1.5rem;font-weight:800}
    .stat .l{color:var(--muted);font-size:.92rem;margin-top:4px}
    .mini{
      padding:18px;border-radius:22px;background:linear-gradient(180deg, rgba(155,92,255,.14), rgba(59,130,246,.08));
      border:1px solid rgba(155,92,255,.18)
    }
    .mini h3{margin:0 0 8px}
    .mini p{margin:0;color:var(--muted);line-height:1.6}

    .grid2{display:grid;grid-template-columns:1fr 1fr;gap:22px;margin:20px 0}
    .section{padding:24px}
    .section h2{margin:0 0 10px;font-size:1.5rem}
    .section p.lead{margin:0 0 18px;color:var(--muted);line-height:1.7}

    .controls{display:grid;grid-template-columns:1.3fr .7fr .7fr auto;gap:12px;margin-bottom:16px}
    .field{
      width:100%;padding:14px 15px;border-radius:16px;border:1px solid var(--line);
      background:rgba(255,255,255,.04);color:var(--text);outline:none;
    }
    .field::placeholder{color:#7d86af}
    .field:focus{border-color:rgba(155,92,255,.55);box-shadow:0 0 0 4px rgba(155,92,255,.12)}
    select.field{cursor:pointer}

    .cards{display:grid;grid-template-columns:repeat(2,1fr);gap:14px}
    .card{
      padding:18px;border-radius:22px;border:1px solid var(--line);background:rgba(255,255,255,.04);
      position:relative;overflow:hidden;
    }
    .card::before{
      content:"";position:absolute;inset:auto -40px -40px auto;width:110px;height:110px;border-radius:50%;
      background:radial-gradient(circle, rgba(155,92,255,.24), transparent 60%);
    }
    .card-top{display:flex;justify-content:space-between;gap:12px;align-items:flex-start}
    .badge{padding:7px 10px;border-radius:999px;font-size:12px;font-weight:700}
    .b-safe{background:rgba(41,211,156,.12);color:#9df6d9;border:1px solid rgba(41,211,156,.18)}
    .b-new{background:rgba(59,130,246,.12);color:#b7d3ff;border:1px solid rgba(59,130,246,.18)}
    .b-hot{background:rgba(155,92,255,.12);color:#e2d0ff;border:1px solid rgba(155,92,255,.18)}
    .title{margin:12px 0 8px;font-weight:800;font-size:1.08rem}
    .desc{color:var(--muted);line-height:1.65;font-size:.95rem}
    .meta{display:flex;gap:10px;flex-wrap:wrap;margin-top:14px;color:#aeb8df;font-size:.87rem}
    .card-actions{display:flex;gap:10px;margin-top:16px;flex-wrap:wrap}
    .tiny{
      padding:10px 12px;border-radius:12px;border:1px solid var(--line);background:rgba(255,255,255,.03);
      color:var(--text);cursor:pointer;
    }
    .tiny:hover{background:rgba(255,255,255,.07)}
    .tiny.danger{border-color:rgba(255,95,122,.2);background:rgba(255,95,122,.08)}

    .formgrid{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    textarea.field{min-height:120px;resize:vertical}
    .full{grid-column:1/-1}
    .hint{font-size:.9rem;color:var(--muted);margin-top:12px;line-height:1.6}

    .footer{
      margin:22px 0 8px;padding:18px;color:var(--muted);text-align:center;
      border-top:1px solid var(--line)
    }

    .modal-backdrop{
      position:fixed;inset:0;background:rgba(2,4,13,.7);display:none;align-items:center;justify-content:center;
      padding:18px;z-index:50;
    }
    .modal{max-width:680px;width:100%;border-radius:28px;background:linear-gradient(180deg, #11172d, #0d1121);border:1px solid var(--line);box-shadow:var(--shadow);overflow:hidden}
    .modal-head{display:flex;justify-content:space-between;align-items:center;gap:10px;padding:18px 20px;border-bottom:1px solid var(--line)}
    .modal-body{padding:20px}
    .close{background:transparent;border:none;color:var(--text);font-size:28px;cursor:pointer;line-height:1}
    .pillrow{display:flex;gap:8px;flex-wrap:wrap;margin:12px 0 0}
    .pill{padding:8px 10px;border-radius:999px;background:rgba(255,255,255,.05);border:1px solid var(--line);color:#cfd6ff;font-size:12px}

    @media (max-width: 920px){
      .hero,.grid2,.cards,.controls,.formgrid{grid-template-columns:1fr}
      .nav{border-radius:24px;position:static}
      .navlinks{justify-content:flex-start}
    }
  </style>
</head>
<body>
  <div class="wrap">
    <nav class="nav">
      <div class="brand"><div class="logo">DX</div><div>DXDupes</div></div>
      <div class="navlinks">
        <a href="#home">Home</a>
        <a href="#dupes">Dupe Log</a>
        <a href="#submit">Submit</a>
        <a href="#about">About</a>
      </div>
    </nav>

    <main id="home" class="hero">
      <section class="panel hero-main">
        <span class="eyebrow">⚡ GitHub Pages ready • clean • responsive</span>
        <h1><span class="grad">DXDupes</span><br/>a sleek dupe log website</h1>
        <p class="sub">A simple, polished website for showcasing dupes, updates, notes, and submissions. Everything works in one file, saves locally in the browser, and is easy to publish on GitHub Pages.</p>
        <div class="actions">
          <button class="btn btn-primary" onclick="document.getElementById('dupes').scrollIntoView({behavior:'smooth'})">View Dupe Log</button>
          <button class="btn btn-ghost" onclick="resetDemo()">Reset Demo Data</button>
        </div>
      </section>

      <aside class="panel hero-side">
        <div class="statgrid">
          <div class="stat"><div class="n" id="countTotal">0</div><div class="l">Total entries</div></div>
          <div class="stat"><div class="n" id="countFeatured">0</div><div class="l">Featured</div></div>
        </div>
        <div class="mini">
          <h3>Works out of the box</h3>
          <p>No backend needed. Search, filter, add, delete, and open details all work using localStorage.</p>
        </div>
      </aside>
    </main>

    <section id="dupes" class="panel section">
      <h2>Dupe Log</h2>
      <p class="lead">Browse entries, search by title, or filter by category and status.</p>

      <div class="controls">
        <input id="search" class="field" type="text" placeholder="Search entries..." />
        <select id="filterCategory" class="field">
          <option value="all">All categories</option>
        </select>
        <select id="filterSort" class="field">
          <option value="newest">Newest first</option>
          <option value="oldest">Oldest first</option>
          <option value="title">Title A-Z</option>
        </select>
        <button class="btn btn-primary" id="clearFilters">Clear</button>
      </div>

      <div id="cards" class="cards"></div>
    </section>

    <div class="grid2">
      <section id="submit" class="panel section">
        <h2>Submit an entry</h2>
        <p class="lead">Add a new dupe note or update to the log. It saves instantly in the browser.</p>
        <form id="entryForm">
          <div class="formgrid">
            <input class="field" id="title" placeholder="Title" required />
            <input class="field" id="category" placeholder="Category" required />
            <input class="field full" id="status" placeholder="Status label, e.g. Verified" required />
            <textarea class="field full" id="description" placeholder="Description" required></textarea>
            <input class="field" id="tags" placeholder="Tags, comma separated" />
            <select class="field" id="featured">
              <option value="no">Not featured</option>
              <option value="yes">Featured</option>
            </select>
          </div>
          <div class="actions" style="margin-top:14px">
            <button class="btn btn-primary" type="submit">Add entry</button>
            <button class="btn btn-ghost" type="button" id="fillDemo">Fill example</button>
          </div>
          <div class="hint">Tip: after publishing on GitHub Pages, this site will work without any extra services.</div>
        </form>
      </section>

      <section id="about" class="panel section">
        <h2>About</h2>
        <p class="lead">This is a static site template with a dark purple/blue theme, built for GitHub Pages.</p>
        <div class="mini" style="margin-bottom:14px">
          <h3>Included features</h3>
          <p>Mobile layout, modal details, local saving, search, category filter, sort options, and delete buttons.</p>
        </div>
        <div class="mini">
          <h3>GitHub Pages setup</h3>
          <p>Name the file <strong>index.html</strong>, push it to a repository, then enable GitHub Pages from the repo settings.</p>
        </div>
      </section>
    </div>

    <div class="footer">DXDupes • made for GitHub Pages • static single-file site</div>
  </div>

  <div class="modal-backdrop" id="modalBackdrop" aria-hidden="true">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
      <div class="modal-head">
        <strong id="modalTitle">Entry Details</strong>
        <button class="close" id="closeModal" aria-label="Close">&times;</button>
      </div>
      <div class="modal-body" id="modalBody"></div>
    </div>
  </div>

  <script>
    const STORAGE_KEY = 'dxdupes_entries_v1';

    const demoEntries = [
      {
        id: crypto.randomUUID(),
        title: 'Starter Dupe Pack',
        category: 'Verified',
        status: 'Hot',
        description: 'A sample entry showing how an item looks in the log. Replace this with your own dupe notes or updates.',
        tags: ['sample', 'verified', 'starter'],
        featured: true,
        createdAt: Date.now() - 86400000 * 2
      },
      {
        id: crypto.randomUUID(),
        title: 'Update Notice',
        category: 'News',
        status: 'New',
        description: 'Use this section for announcements, changes, or patch notes. Everything can be edited from the browser.',
        tags: ['news', 'update'],
        featured: false,
        createdAt: Date.now() - 86400000
      }
    ];

    const els = {
      cards: document.getElementById('cards'),
      search: document.getElementById('search'),
      filterCategory: document.getElementById('filterCategory'),
      filterSort: document.getElementById('filterSort'),
      clearFilters: document.getElementById('clearFilters'),
      total: document.getElementById('countTotal'),
      featured: document.getElementById('countFeatured'),
      form: document.getElementById('entryForm'),
      title: document.getElementById('title'),
      category: document.getElementById('category'),
      status: document.getElementById('status'),
      description: document.getElementById('description'),
      tags: document.getElementById('tags'),
      featuredSelect: document.getElementById('featured'),
      fillDemo: document.getElementById('fillDemo'),
      modalBackdrop: document.getElementById('modalBackdrop'),
      modalBody: document.getElementById('modalBody'),
      closeModal: document.getElementById('closeModal')
    };

    function loadEntries(){
      const saved = localStorage.getItem(STORAGE_KEY);
      if (!saved) {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(demoEntries));
        return [...demoEntries];
      }
      try {
        const parsed = JSON.parse(saved);
        return Array.isArray(parsed) ? parsed : [...demoEntries];
      } catch {
        return [...demoEntries];
      }
    }

    function saveEntries(entries){
      localStorage.setItem(STORAGE_KEY, JSON.stringify(entries));
    }

    let entries = loadEntries();

    function statusClass(status){
      const s = (status || '').toLowerCase();
      if (s.includes('hot')) return 'b-hot';
      if (s.includes('new')) return 'b-new';
      return 'b-safe';
    }

    function categoryOptions(){
      const cats = [...new Set(entries.map(e => e.category))].sort((a,b)=>a.localeCompare(b));
      const current = els.filterCategory.value || 'all';
      els.filterCategory.innerHTML = '<option value="all">All categories</option>' + cats.map(c => `<option value="${escapeHtml(c)}">${escapeHtml(c)}</option>`).join('');
      els.filterCategory.value = cats.includes(current) ? current : 'all';
    }

    function escapeHtml(str){
      return String(str)
        .replaceAll('&','&amp;')
        .replaceAll('<','&lt;')
        .replaceAll('>','&gt;')
        .replaceAll('"','&quot;')
        .replaceAll("'",'&#39;');
    }

    function filteredEntries(){
      const q = els.search.value.trim().toLowerCase();
      const cat = els.filterCategory.value;
      let result = entries.filter(e => {
        const hay = [e.title, e.category, e.status, e.description, ...(e.tags || [])].join(' ').toLowerCase();
        const matchesQuery = !q || hay.includes(q);
        const matchesCat = cat === 'all' || e.category === cat;
        return matchesQuery && matchesCat;
      });

      switch (els.filterSort.value) {
        case 'oldest': result.sort((a,b)=>a.createdAt-b.createdAt); break;
        case 'title': result.sort((a,b)=>a.title.localeCompare(b.title)); break;
        default: result.sort((a,b)=>b.createdAt-a.createdAt); break;
      }
      return result;
    }

    function render(){
      categoryOptions();
      const list = filteredEntries();
      els.total.textContent = entries.length;
      els.featured.textContent = entries.filter(e => e.featured).length;

      if (!list.length) {
        els.cards.innerHTML = `<div class="card full"><div class="title">No entries found</div><div class="desc">Try changing the search or filter.</div></div>`;
        return;
      }

      els.cards.innerHTML = list.map(e => `
        <article class="card">
          <div class="card-top">
            <span class="badge ${statusClass(e.status)}">${escapeHtml(e.status || 'Entry')}</span>
            ${e.featured ? '<span class="badge b-new">Featured</span>' : ''}
          </div>
          <div class="title">${escapeHtml(e.title)}</div>
          <div class="desc">${escapeHtml(e.description)}</div>
          <div class="meta">
            <span>Category: ${escapeHtml(e.category)}</span>
            <span>•</span>
            <span>${new Date(e.createdAt).toLocaleDateString()}</span>
          </div>
          <div class="pillrow">${(e.tags || []).map(t => `<span class="pill">#${escapeHtml(t.trim())}</span>`).join('')}</div>
          <div class="card-actions">
            <button class="tiny" data-action="view" data-id="${e.id}">View</button>
            <button class="tiny" data-action="copy" data-id="${e.id}">Copy JSON</button>
            <button class="tiny danger" data-action="delete" data-id="${e.id}">Delete</button>
          </div>
        </article>
      `).join('');
    }

    function openModal(entry){
      els.modalBody.innerHTML = `
        <p><strong>Title:</strong> ${escapeHtml(entry.title)}</p>
        <p><strong>Category:</strong> ${escapeHtml(entry.category)}</p>
        <p><strong>Status:</strong> ${escapeHtml(entry.status)}</p>
        <p><strong>Description:</strong> ${escapeHtml(entry.description)}</p>
        <p><strong>Tags:</strong> ${escapeHtml((entry.tags || []).join(', ') || 'None')}</p>
        <p><strong>Featured:</strong> ${entry.featured ? 'Yes' : 'No'}</p>
        <p><strong>Created:</strong> ${new Date(entry.createdAt).toLocaleString()}</p>
      `;
      els.modalBackdrop.style.display = 'flex';
      els.modalBackdrop.setAttribute('aria-hidden', 'false');
    }

    function closeModal(){
      els.modalBackdrop.style.display = 'none';
      els.modalBackdrop.setAttribute('aria-hidden', 'true');
    }

    function resetDemo(){
      if (!confirm('Reset the website data back to the demo entries?')) return;
      entries = [...demoEntries];
      saveEntries(entries);
      render();
    }
    window.resetDemo = resetDemo;

    els.cards.addEventListener('click', async (ev) => {
      const btn = ev.target.closest('button[data-action]');
      if (!btn) return;
      const id = btn.dataset.id;
      const entry = entries.find(e => e.id === id);
      if (!entry) return;

      const action = btn.dataset.action;
      if (action === 'view') openModal(entry);
      if (action === 'copy') {
        await navigator.clipboard.writeText(JSON.stringify(entry, null, 2));
        btn.textContent = 'Copied!';
        setTimeout(() => btn.textContent = 'Copy JSON', 900);
      }
      if (action === 'delete') {
        if (!confirm(`Delete "${entry.title}"?`)) return;
        entries = entries.filter(e => e.id !== id);
        saveEntries(entries);
        render();
      }
    });

    els.form.addEventListener('submit', (ev) => {
      ev.preventDefault();
      const newEntry = {
        id: crypto.randomUUID(),
        title: els.title.value.trim(),
        category: els.category.value.trim(),
        status: els.status.value.trim(),
        description: els.description.value.trim(),
        tags: els.tags.value.split(',').map(t => t.trim()).filter(Boolean),
        featured: els.featuredSelect.value === 'yes',
        createdAt: Date.now()
      };

      if (!newEntry.title || !newEntry.category || !newEntry.status || !newEntry.description) {
        alert('Please fill in title, category, status, and description.');
        return;
      }

      entries.unshift(newEntry);
      saveEntries(entries);
      render();
      els.form.reset();
      els.title.focus();
      document.getElementById('dupes').scrollIntoView({behavior:'smooth'});
    });

    els.fillDemo.addEventListener('click', () => {
      els.title.value = 'Example Entry';
      els.category.value = 'Update';
      els.status.value = 'Verified';
      els.description.value = 'This is a quick example entry for testing the form.';
      els.tags.value = 'example, test, demo';
      els.featuredSelect.value = 'yes';
    });

    els.search.addEventListener('input', render);
    els.filterCategory.addEventListener('change', render);
    els.filterSort.addEventListener('change', render);
    els.clearFilters.addEventListener('click', () => {
      els.search.value = '';
      els.filterCategory.value = 'all';
      els.filterSort.value = 'newest';
      render();
    });

    els.closeModal.addEventListener('click', closeModal);
    els.modalBackdrop.addEventListener('click', (e) => {
      if (e.target === els.modalBackdrop) closeModal();
    });
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') closeModal();
    });

    render();
  </script>
</body>
</html>
