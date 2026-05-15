<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>DXDupes</title>
  <style>
    :root {
      --bg: #070814;
      --panel: rgba(16, 19, 35, 0.9);
      --panel-2: rgba(255, 255, 255, 0.04);
      --line: rgba(255,255,255,0.08);
      --text: #eef1ff;
      --muted: #a3abc9;
      --purple: #8b5cf6;
      --purple-2: #6d28d9;
      --blue: #3b82f6;
      --green: #22c55e;
      --red: #ef4444;
      --shadow: 0 18px 55px rgba(0,0,0,0.38);
      --radius: 22px;
    }

    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      margin: 0;
      font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      color: var(--text);
      background:
        radial-gradient(circle at top left, rgba(139,92,246,0.22), transparent 24%),
        radial-gradient(circle at top right, rgba(59,130,246,0.18), transparent 24%),
        linear-gradient(180deg, #05060f 0%, var(--bg) 100%);
      min-height: 100vh;
    }

    a { color: inherit; text-decoration: none; }
    button, input, textarea, select { font: inherit; }

    .wrap { max-width: 1320px; margin: 0 auto; padding: 18px; }

    .nav {
      display: flex; align-items: center; justify-content: space-between; gap: 16px;
      padding: 14px 18px; margin-bottom: 22px;
      background: rgba(10, 12, 24, 0.8);
      border: 1px solid var(--line);
      border-radius: 999px;
      backdrop-filter: blur(16px);
      box-shadow: var(--shadow);
      position: sticky; top: 12px; z-index: 20;
    }
    .brand { display: flex; align-items: center; gap: 12px; font-weight: 900; }
    .logo {
      width: 40px; height: 40px; border-radius: 14px;
      display: grid; place-items: center;
      background: linear-gradient(135deg, var(--purple), var(--blue));
      color: white; font-weight: 900;
    }
    .navlinks { display: flex; gap: 14px; flex-wrap: wrap; }
    .navlinks a { padding: 10px 12px; border-radius: 999px; color: var(--muted); }
    .navlinks a:hover { background: rgba(255,255,255,0.06); color: var(--text); }

    .hero {
      display: grid;
      grid-template-columns: 1.2fr 0.8fr;
      gap: 20px;
      margin-bottom: 20px;
    }
    .panel {
      background: linear-gradient(180deg, rgba(16, 19, 35, 0.94), rgba(11, 14, 27, 0.94));
      border: 1px solid var(--line);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
    }
    .hero-main { padding: 34px; }
    .eyebrow {
      display: inline-flex; gap: 8px; align-items: center;
      padding: 8px 12px; border-radius: 999px;
      background: rgba(139,92,246,0.12);
      border: 1px solid rgba(139,92,246,0.22);
      color: #dbcaff; font-size: 13px;
    }
    h1 {
      margin: 16px 0 10px;
      font-size: clamp(2.4rem, 5vw, 4.8rem);
      line-height: 0.98;
    }
    .grad {
      background: linear-gradient(90deg, #ffffff, var(--purple), var(--blue));
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }
    .sub { color: var(--muted); line-height: 1.75; max-width: 62ch; font-size: 1.02rem; }
    .actions { display: flex; gap: 12px; flex-wrap: wrap; margin-top: 22px; }
    .btn {
      border: none; cursor: pointer; border-radius: 16px;
      padding: 13px 16px; font-weight: 700;
      display: inline-flex; align-items: center; gap: 10px;
      transition: transform 0.18s ease, opacity 0.18s ease;
    }
    .btn:hover { transform: translateY(-1px); }
    .btn-primary { background: linear-gradient(135deg, var(--purple), var(--blue)); color: white; }
    .btn-ghost { background: rgba(255,255,255,0.05); color: var(--text); border: 1px solid var(--line); }
    .btn-danger { background: transparent; color: #ff8a8a; border: 1px solid rgba(239,68,68,0.4); }

    .hero-side { padding: 18px; display: grid; gap: 14px; }
    .statgrid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
    .stat, .mini {
      padding: 18px; border-radius: 22px; background: rgba(255,255,255,0.04); border: 1px solid var(--line);
    }
    .stat .n { font-size: 1.55rem; font-weight: 900; }
    .stat .l { color: var(--muted); margin-top: 4px; font-size: 0.92rem; }
    .mini h3 { margin: 0 0 8px; }
    .mini p { margin: 0; color: var(--muted); line-height: 1.6; }

    .section { padding: 24px; margin-bottom: 20px; }
    .section h2 { margin: 0 0 8px; font-size: 1.5rem; }
    .lead { margin: 0 0 16px; color: var(--muted); line-height: 1.7; }

    .controls {
      display: grid;
      grid-template-columns: 1.4fr 0.8fr 0.8fr auto;
      gap: 12px;
      margin-bottom: 16px;
    }
    .field {
      width: 100%; padding: 14px 15px; border-radius: 16px;
      border: 1px solid var(--line); outline: none;
      background: rgba(255,255,255,0.04); color: var(--text);
    }
    .field::placeholder { color: #7f89aa; }
    .field:focus { border-color: rgba(139,92,246,0.55); box-shadow: 0 0 0 4px rgba(139,92,246,0.10); }
    textarea.field { min-height: 118px; resize: vertical; }

    .cards {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 14px;
    }
    .card {
      padding: 18px;
      border-radius: 22px;
      border: 1px solid var(--line);
      background: rgba(255,255,255,0.04);
      overflow: hidden;
    }
    .card-top { display: flex; justify-content: space-between; gap: 10px; align-items: flex-start; }
    .badge {
      display: inline-flex; align-items: center; gap: 6px;
      padding: 7px 10px; border-radius: 999px; font-size: 12px; font-weight: 800;
      border: 1px solid rgba(139,92,246,0.18); background: rgba(139,92,246,0.12); color: #dcc8ff;
    }
    .title { margin: 12px 0 8px; font-size: 1.08rem; font-weight: 900; }
    .desc { color: var(--muted); line-height: 1.6; font-size: 0.95rem; }
    .meta { display: flex; gap: 10px; flex-wrap: wrap; margin-top: 12px; color: #b2b9d8; font-size: 0.88rem; }
    .pillrow { display: flex; gap: 8px; flex-wrap: wrap; margin-top: 12px; }
    .pill {
      padding: 7px 10px; border-radius: 999px; background: rgba(255,255,255,0.05);
      border: 1px solid var(--line); color: #d5dbf7; font-size: 12px;
    }
    .filebox {
      margin-top: 14px; padding-top: 14px; border-top: 1px solid var(--line);
      display: grid; gap: 8px;
    }
    .fileline {
      display: flex; justify-content: space-between; gap: 10px; align-items: center;
      padding: 10px 0; color: #d9def1;
    }
    .fileline span:last-child { color: var(--muted); }
    .preview-grid {
      display: grid; grid-template-columns: repeat(auto-fit, minmax(110px, 1fr)); gap: 10px; margin-top: 12px;
    }
    .preview-grid img {
      width: 100%; height: 96px; object-fit: cover; border-radius: 14px; border: 1px solid var(--line);
    }
    .card-actions { display: flex; gap: 10px; margin-top: 14px; flex-wrap: wrap; }
    .tiny {
      padding: 10px 12px; border-radius: 12px; border: 1px solid var(--line);
      background: rgba(255,255,255,0.04); color: var(--text); cursor: pointer;
    }
    .tiny:hover { background: rgba(255,255,255,0.07); }

    .grid2 { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 20px; }
    .formgrid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
    .full { grid-column: 1 / -1; }
    .hint { margin-top: 12px; color: var(--muted); line-height: 1.6; font-size: 0.92rem; }
    .upload-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }

    .footer {
      padding: 18px 8px 8px;
      text-align: center;
      color: var(--muted);
    }

    .modal-backdrop {
      position: fixed; inset: 0; display: none;
      align-items: center; justify-content: center;
      background: rgba(1,3,10,0.72); z-index: 50; padding: 16px;
    }
    .modal {
      width: 100%; max-width: 760px; border-radius: 26px;
      background: linear-gradient(180deg, #11172d, #0d1020);
      border: 1px solid var(--line);
      box-shadow: var(--shadow);
      overflow: hidden;
    }
    .modal-head {
      display: flex; justify-content: space-between; align-items: center; gap: 10px;
      padding: 18px 20px; border-bottom: 1px solid var(--line);
    }
    .modal-body { padding: 20px; color: var(--text); }
    .close { border: none; background: transparent; color: var(--text); font-size: 30px; cursor: pointer; line-height: 1; }

    @media (max-width: 1100px) {
      .hero, .grid2, .cards { grid-template-columns: 1fr; }
      .controls { grid-template-columns: 1fr 1fr; }
    }
    @media (max-width: 700px) {
      .nav { border-radius: 24px; position: static; }
      .controls, .formgrid, .upload-row, .statgrid { grid-template-columns: 1fr; }
      .cards { grid-template-columns: 1fr; }
      .hero-main { padding: 24px; }
    }
  </style>
</head>
<body>
  <div class="wrap">
    <nav class="nav">
      <div class="brand">
        <div class="logo">DX</div>
        <div>DXDupes</div>
      </div>
      <div class="navlinks">
        <a href="#home">Home</a>
        <a href="#dupes">Browse</a>
        <a href="#submit">Add Dupe</a>
        <a href="#about">About</a>
      </div>
    </nav>

    <main id="home" class="hero">
      <section class="panel hero-main">
        <span class="eyebrow">⚡ GitHub Pages ready • single file • responsive</span>
        <h1><span class="grad">DX</span>Dupes</h1>
        <p class="sub">This is where you get your dupes (files). Upload, share, and browse entries in a clean dark layout. Everything works in one HTML file and saves locally in the browser.</p>
        <div class="actions">
          <button class="btn btn-primary" onclick="document.getElementById('dupes').scrollIntoView({behavior:'smooth'})">View Dupe Log</button>
          <button class="btn btn-ghost" id="resetDemoBtn">Reset Demo Data</button>
        </div>
      </section>

      <aside class="panel hero-side">
        <div class="statgrid">
          <div class="stat"><div class="n" id="totalCount">0</div><div class="l">Total entries</div></div>
          <div class="stat"><div class="n" id="featuredCount">0</div><div class="l">Featured</div></div>
        </div>
        <div class="mini">
          <h3>Upload works</h3>
          <p>Add files and screenshots from the form below. Screenshots are previewed inside the entry.</p>
        </div>
      </aside>
    </main>

    <section id="dupes" class="panel section">
      <h2>Dupe Log</h2>
      <p class="lead">Search, filter, sort, and open details for each entry.</p>

      <div class="controls">
        <input id="search" class="field" type="text" placeholder="Search dupes..." />
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
        <h2>Add Dupe</h2>
        <p class="lead">Post a new dupe entry with files and screenshots. On GitHub Pages, this works locally in the browser.</p>
        <form id="entryForm">
          <div class="formgrid">
            <input class="field" id="title" placeholder="Title" required />
            <input class="field" id="category" placeholder="Category" required />
            <textarea class="field full" id="description" placeholder="Description" required></textarea>
            <input class="field full" id="tags" placeholder="Tags, comma separated" />
            <div class="upload-row full">
              <input class="field" id="fileUpload" type="file" multiple />
              <input class="field" id="screenshotUpload" type="file" accept="image/*" multiple />
            </div>
            <select class="field full" id="featured">
              <option value="no">Not featured</option>
              <option value="yes">Featured</option>
            </select>
          </div>
          <div class="actions" style="margin-top:14px;">
            <button class="btn btn-primary" type="submit">Add Entry</button>
            <button class="btn btn-ghost" type="button" id="fillDemo">Fill Example</button>
          </div>
          <div class="hint">Uploaded screenshots are saved as images in the browser. Uploaded files are stored as file names and file details for the demo version.</div>
        </form>
      </section>

      <section id="about" class="panel section">
        <h2>About</h2>
        <p class="lead">A clean dupe-log template for GitHub Pages with a dark purple theme.</p>
        <div class="mini" style="margin-bottom: 14px;">
          <h3>Features</h3>
          <p>Search, category filters, sorting, add entries, delete entries, screenshots, and local saving.</p>
        </div>
        <div class="mini">
          <h3>Publish</h3>
          <p>Save this file as <strong>index.html</strong>, push it to GitHub, then turn on GitHub Pages in repo settings.</p>
        </div>
      </section>
    </div>

    <div class="footer">DXDupes • GitHub Pages template • static single-file site</div>
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
    const STORAGE_KEY = 'dxdupes_entries_v2';

    const demoEntries = [
      {
        id: crypto.randomUUID(),
        title: 'Starter Dupe Pack',
        category: 'Verified',
        description: 'Example entry showing how your dupe post will look.',
        tags: ['sample', 'demo', 'starter'],
        featured: true,
        createdAt: Date.now() - 86400000 * 2,
        files: [{ name: 'starter_pack.json', size: '12.4 KB' }],
        screenshots: []
      },
      {
        id: crypto.randomUUID(),
        title: 'Update Notice',
        category: 'News',
        description: 'Use this section for announcements and updates.',
        tags: ['news', 'update'],
        featured: false,
        createdAt: Date.now() - 86400000,
        files: [],
        screenshots: []
      }
    ];

    const els = {
      cards: document.getElementById('cards'),
      search: document.getElementById('search'),
      filterCategory: document.getElementById('filterCategory'),
      filterSort: document.getElementById('filterSort'),
      clearFilters: document.getElementById('clearFilters'),
      totalCount: document.getElementById('totalCount'),
      featuredCount: document.getElementById('featuredCount'),
      form: document.getElementById('entryForm'),
      title: document.getElementById('title'),
      category: document.getElementById('category'),
      description: document.getElementById('description'),
      tags: document.getElementById('tags'),
      fileUpload: document.getElementById('fileUpload'),
      screenshotUpload: document.getElementById('screenshotUpload'),
      featured: document.getElementById('featured'),
      fillDemo: document.getElementById('fillDemo'),
      resetDemoBtn: document.getElementById('resetDemoBtn'),
      modalBackdrop: document.getElementById('modalBackdrop'),
      modalBody: document.getElementById('modalBody'),
      closeModal: document.getElementById('closeModal')
    };

    function escapeHtml(str) {
      return String(str)
        .replaceAll('&', '&amp;')
        .replaceAll('<', '&lt;')
        .replaceAll('>', '&gt;')
        .replaceAll('"', '&quot;')
        .replaceAll("'", '&#39;');
    }

    function loadEntries() {
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

    function saveEntries() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(entries));
    }

    let entries = loadEntries();

    function statusBadge(entry) {
      return entry.featured ? 'Featured' : 'Entry';
    }

    function fillCategoryOptions() {
      const current = els.filterCategory.value || 'all';
      const cats = [...new Set(entries.map(e => e.category))].sort((a, b) => a.localeCompare(b));
      els.filterCategory.innerHTML = '<option value="all">All categories</option>' +
        cats.map(c => `<option value="${escapeHtml(c)}">${escapeHtml(c)}</option>`).join('');
      els.filterCategory.value = cats.includes(current) ? current : 'all';
    }

    function getFilteredEntries() {
      const q = els.search.value.trim().toLowerCase();
      const cat = els.filterCategory.value;
      let result = entries.filter(entry => {
        const haystack = [entry.title, entry.category, entry.description, ...(entry.tags || []), ...(entry.files || []).map(f => f.name)].join(' ').toLowerCase();
        const matchesSearch = !q || haystack.includes(q);
        const matchesCategory = cat === 'all' || entry.category === cat;
        return matchesSearch && matchesCategory;
      });

      if (els.filterSort.value === 'oldest') {
        result.sort((a, b) => a.createdAt - b.createdAt);
      } else if (els.filterSort.value === 'title') {
        result.sort((a, b) => a.title.localeCompare(b.title));
      } else {
        result.sort((a, b) => b.createdAt - a.createdAt);
      }
      return result;
    }

    function render() {
      fillCategoryOptions();
      const list = getFilteredEntries();
      els.totalCount.textContent = entries.length;
      els.featuredCount.textContent = entries.filter(e => e.featured).length;

      if (!list.length) {
        els.cards.innerHTML = '<div class="card"><div class="title">No entries found</div><div class="desc">Try a different search or filter.</div></div>';
        return;
      }

      els.cards.innerHTML = list.map(entry => {
        const tags = (entry.tags || []).map(t => `<span class="pill">#${escapeHtml(t)}</span>`).join('');
        const files = (entry.files || []).length
          ? entry.files.map(f => `<div class="fileline"><span>📄 ${escapeHtml(f.name)}</span><span>${escapeHtml(f.size || '')}</span></div>`).join('')
          : '<div class="fileline"><span>No files attached</span><span></span></div>';
        const screenshots = (entry.screenshots || []).length
          ? `<div class="preview-grid">${entry.screenshots.map(s => `<img src="${s.dataUrl}" alt="${escapeHtml(s.name)}" />`).join('')}</div>`
          : '';

        return `
          <article class="card">
            <div class="card-top">
              <span class="badge">${escapeHtml(statusBadge(entry))}</span>
              ${entry.featured ? '<span class="badge">Top</span>' : ''}
            </div>
            <div class="title">${escapeHtml(entry.title)}</div>
            <div class="desc">${escapeHtml(entry.description)}</div>
            <div class="meta">
              <span>Category: ${escapeHtml(entry.category)}</span>
              <span>•</span>
              <span>${new Date(entry.createdAt).toLocaleDateString()}</span>
            </div>
            <div class="pillrow">${tags}</div>
            <div class="filebox">${files}</div>
            ${screenshots}
            <div class="card-actions">
              <button class="tiny" data-action="view" data-id="${entry.id}">Details</button>
              <button class="tiny" data-action="download" data-id="${entry.id}">Download</button>
              <button class="tiny btn-danger" data-action="delete" data-id="${entry.id}">Delete</button>
            </div>
          </article>
        `;
      }).join('');
    }

    function openModal(entry) {
      const screenshots = (entry.screenshots || []).length
        ? `<div class="preview-grid" style="margin-top:14px;">${entry.screenshots.map(s => `<img src="${s.dataUrl}" alt="${escapeHtml(s.name)}" />`).join('')}</div>`
        : '<p style="color: var(--muted);">No screenshots attached.</p>';

      els.modalBody.innerHTML = `
        <p><strong>Title:</strong> ${escapeHtml(entry.title)}</p>
        <p><strong>Category:</strong> ${escapeHtml(entry.category)}</p>
        <p><strong>Description:</strong> ${escapeHtml(entry.description)}</p>
        <p><strong>Tags:</strong> ${escapeHtml((entry.tags || []).join(', ') || 'None')}</p>
        <p><strong>Featured:</strong> ${entry.featured ? 'Yes' : 'No'}</p>
        <p><strong>Created:</strong> ${new Date(entry.createdAt).toLocaleString()}</p>
        <p><strong>Files:</strong> ${(entry.files || []).length ? entry.files.map(f => `${escapeHtml(f.name)} (${escapeHtml(f.size || '')})`).join('<br>') : 'No files attached'}</p>
        <div style="margin-top:14px;"><strong>Screenshots:</strong>${screenshots}</div>
      `;
      els.modalBackdrop.style.display = 'flex';
      els.modalBackdrop.setAttribute('aria-hidden', 'false');
    }

    function closeModal() {
      els.modalBackdrop.style.display = 'none';
      els.modalBackdrop.setAttribute('aria-hidden', 'true');
    }

    function resetDemo() {
      if (!confirm('Reset the site data back to the demo entries?')) return;
      entries = [...demoEntries];
      saveEntries();
      render();
    }

    async function filesToList(fileList) {
      const files = Array.from(fileList || []);
      const results = [];

      for (const file of files) {
        const dataUrl = await new Promise((resolve, reject) => {
          const reader = new FileReader();
          reader.onload = () => resolve(reader.result);
          reader.onerror = reject;
          reader.readAsDataURL(file);
        });

        results.push({
          name: file.name,
          size: `${(file.size / 1024).toFixed(1)} KB`,
          type: file.type || 'application/octet-stream',
          dataUrl
        });
      }

      return results;
    }

    async function screenshotsToList(fileList) {
      const files = Array.from(fileList || []);
      const results = [];
      for (const file of files) {
        const dataUrl = await new Promise((resolve, reject) => {
          const reader = new FileReader();
          reader.onload = () => resolve(reader.result);
          reader.onerror = reject;
          reader.readAsDataURL(file);
        });
        results.push({ name: file.name, dataUrl });
      }
      return results;
    }

    els.cards.addEventListener('click', async (ev) => {
      const btn = ev.target.closest('button[data-action]');
      if (!btn) return;
      const entry = entries.find(e => e.id === btn.dataset.id);
      if (!entry) return;

      const action = btn.dataset.action;

      if (action === 'view') {
        openModal(entry);
      }

      if (action === 'delete') {
        if (!confirm(`Delete "${entry.title}"?`)) return;
        entries = entries.filter(e => e.id !== entry.id);
        saveEntries();
        render();
      }

      if (action === 'download') {
        if (!entry.files || !entry.files.length) {
          alert('No downloadable files attached.');
          return;
        }

        entry.files.forEach(file => {
          const a = document.createElement('a');
          a.href = file.dataUrl;
          a.download = file.name;
          document.body.appendChild(a);
          a.click();
          a.remove();
        });
      }
    });

    els.form.addEventListener('submit', async (ev) => {
      ev.preventDefault();

      const title = els.title.value.trim();
      const category = els.category.value.trim();
      const description = els.description.value.trim();
      const tags = els.tags.value.split(',').map(t => t.trim()).filter(Boolean);
      const featured = els.featured.value === 'yes';

      if (!title || !category || !description) {
        alert('Please fill in title, category, and description.');
        return;
      }

      const [files, screenshots] = await Promise.all([
        filesToList(els.fileUpload.files),
        screenshotsToList(els.screenshotUpload.files)
      ]);

      const newEntry = {
        id: crypto.randomUUID(),
        title,
        category,
        description,
        tags,
        featured,
        createdAt: Date.now(),
        files,
        screenshots
      };

      entries.unshift(newEntry);
      saveEntries();
      render();
      els.form.reset();
      els.title.focus();
      document.getElementById('dupes').scrollIntoView({ behavior: 'smooth' });
    });

    els.fillDemo.addEventListener('click', () => {
      els.title.value = 'Example Dupe';
      els.category.value = 'Update';
      els.description.value = 'Example entry used to test the form and upload buttons.';
      els.tags.value = 'example, test, demo';
      els.featured.value = 'yes';
    });

    els.resetDemoBtn.addEventListener('click', resetDemo);
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
