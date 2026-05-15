<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>DXDupes</title>

  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

  <style>
    :root{
      --bg:#070914;
      --bg2:#0d1020;
      --card:#11162a;
      --text:#eef1ff;
      --muted:#a5add0;
      --line:rgba(255,255,255,.08);
      --purple:#9b5cff;
      --blue:#3b82f6;
      --shadow:0 20px 60px rgba(0,0,0,.35);
      --radius:24px;
    }

    *{box-sizing:border-box}

    body{
      margin:0;
      font-family:Inter,Arial,sans-serif;
      background:
      radial-gradient(circle at top left, rgba(155,92,255,.25), transparent 28%),
      radial-gradient(circle at top right, rgba(59,130,246,.20), transparent 28%),
      linear-gradient(180deg,var(--bg),var(--bg2));
      color:var(--text);
      min-height:100vh;
    }

    .wrap{
      max-width:1300px;
      margin:auto;
      padding:20px;
    }

    .nav{
      display:flex;
      justify-content:space-between;
      align-items:center;
      padding:15px 20px;
      border-radius:999px;
      background:rgba(15,18,36,.8);
      border:1px solid var(--line);
      position:sticky;
      top:12px;
      backdrop-filter:blur(14px);
      z-index:100;
    }

    .brand{
      display:flex;
      align-items:center;
      gap:10px;
      font-weight:900;
    }

    .logo{
      width:42px;
      height:42px;
      border-radius:14px;
      background:linear-gradient(135deg,var(--purple),var(--blue));
      display:grid;
      place-items:center;
      font-weight:900;
    }

    .hero{
      margin-top:25px;
      padding:40px;
      border-radius:var(--radius);
      background:rgba(17,22,42,.92);
      border:1px solid var(--line);
      box-shadow:var(--shadow);
    }

    h1{
      font-size:4rem;
      margin:10px 0;
    }

    .grad{
      background:linear-gradient(90deg,#fff,var(--purple),var(--blue));
      -webkit-background-clip:text;
      color:transparent;
    }

    .sub{
      color:var(--muted);
      line-height:1.7;
      max-width:700px;
    }

    .panel{
      background:rgba(17,22,42,.92);
      border:1px solid var(--line);
      border-radius:var(--radius);
      padding:25px;
      margin-top:20px;
      box-shadow:var(--shadow);
    }

    .controls{
      display:grid;
      grid-template-columns:1fr 220px auto;
      gap:12px;
      margin-bottom:18px;
    }

    .field{
      width:100%;
      padding:14px;
      border-radius:16px;
      border:1px solid var(--line);
      background:rgba(255,255,255,.04);
      color:white;
      outline:none;
    }

    textarea.field{
      min-height:120px;
      resize:vertical;
    }

    .btn{
      border:none;
      cursor:pointer;
      border-radius:16px;
      padding:14px 18px;
      font-weight:700;
    }

    .btn-primary{
      background:linear-gradient(135deg,var(--purple),var(--blue));
      color:white;
    }

    .cards{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(320px,1fr));
      gap:16px;
    }

    .card{
      background:rgba(255,255,255,.04);
      border:1px solid var(--line);
      border-radius:22px;
      padding:18px;
    }

    .badge{
      display:inline-block;
      padding:7px 12px;
      border-radius:999px;
      background:rgba(155,92,255,.12);
      border:1px solid rgba(155,92,255,.22);
      color:#dcc8ff;
      font-size:12px;
      font-weight:800;
    }

    .title{
      font-size:1.1rem;
      font-weight:800;
      margin:12px 0 8px;
    }

    .desc{
      color:var(--muted);
      line-height:1.6;
    }

    .preview{
      width:100%;
      border-radius:16px;
      margin-top:14px;
      border:1px solid var(--line);
    }

    .actions{
      display:flex;
      gap:10px;
      margin-top:15px;
      flex-wrap:wrap;
    }

    .tiny{
      border:none;
      border-radius:12px;
      padding:10px 12px;
      cursor:pointer;
      background:rgba(255,255,255,.06);
      color:white;
    }

    .tiny.delete{
      background:rgba(255,0,0,.15);
    }

    .meta{
      margin-top:12px;
      color:var(--muted);
      font-size:.9rem;
    }

    @media(max-width:800px){
      h1{font-size:2.7rem}
      .controls{grid-template-columns:1fr}
    }
  </style>
</head>
<body>

<div class="wrap">

  <div class="nav">
    <div class="brand">
      <div class="logo">DX</div>
      <div>DXDupes</div>
    </div>
  </div>

  <div class="hero">
    <h1><span class="grad">DXDupes</span></h1>
    <p class="sub">
      This is where you get your dupes (files). Upload files and screenshots online with Supabase so everyone can see them.
    </p>
  </div>

  <div class="panel">
    <h2>Upload Dupe</h2>

    <div class="controls">
      <input id="title" class="field" placeholder="Title">
      <input id="category" class="field" placeholder="Category">
      <button class="btn btn-primary" onclick="postDupe()">Post Dupe</button>
    </div>

    <textarea id="description" class="field" placeholder="Description"></textarea>

    <br><br>

    <input id="dupeFile" class="field" type="file">

    <br><br>

    <input id="screenshotFile" class="field" type="file" accept="image/*">
  </div>

  <div class="panel">
    <h2>Dupe Log</h2>
    <div id="cards" class="cards"></div>
  </div>

</div>

<script>

// IMPORTANT:
// You MUST create these in Supabase:
//
// TABLE NAME: dupes
// columns:
// id -> int8 -> primary key
// title -> text
// category -> text
// description -> text
// dupe_url -> text
// screenshot_url -> text
// created_at -> timestamptz
//
// STORAGE BUCKET NAME:
// files
//
// ALSO:
// Make the bucket PUBLIC.
// Turn OFF Row Level Security on the dupes table.

const SUPABASE_URL = 'PASTE_YOUR_SUPABASE_URL';
const SUPABASE_ANON_KEY = 'PASTE_YOUR_SUPABASE_ANON_KEY';

const supabaseClient = supabase.createClient(
  SUPABASE_URL,
  SUPABASE_ANON_KEY
);

async function uploadFile(file, folder){

  if(!file) return '';

  const filePath = `${folder}/${Date.now()}_${file.name}`;

  const { error } = await supabaseClient
    .storage
    .from('files')
    .upload(filePath, file);

  if(error){
    alert(error.message);
    return '';
  }

  return supabaseClient
    .storage
    .from('files')
    .getPublicUrl(filePath)
    .data.publicUrl;
}

async function postDupe(){

  const title = document.getElementById('title').value.trim();
  const category = document.getElementById('category').value.trim();
  const description = document.getElementById('description').value.trim();

  const dupeFile = document.getElementById('dupeFile').files[0];
  const screenshotFile = document.getElementById('screenshotFile').files[0];

  if(!title || !category || !description || !dupeFile){
    alert('Fill everything');
    return;
  }

  const dupeUrl = await uploadFile(dupeFile,'dupes');
  const screenshotUrl = await uploadFile(screenshotFile,'screenshots');

  const { error } = await supabaseClient
    .from('dupes')
    .insert([
      {
        title,
        category,
        description,
        dupe_url:dupeUrl,
        screenshot_url:screenshotUrl,
        created_at:new Date().toISOString()
      }
    ]);

  if(error){
    alert(error.message);
    return;
  }

  document.getElementById('title').value='';
  document.getElementById('category').value='';
  document.getElementById('description').value='';
  document.getElementById('dupeFile').value='';
  document.getElementById('screenshotFile').value='';

  loadDupes();
}

async function deleteDupe(id){

  await supabaseClient
    .from('dupes')
    .delete()
    .eq('id',id);

  loadDupes();
}

async function loadDupes(){

  const { data,error } = await supabaseClient
    .from('dupes')
    .select('*')
    .order('id',{ascending:false});

  if(error){
    console.error(error);
    return;
  }

  const cards = document.getElementById('cards');

  cards.innerHTML='';

  data.forEach(dupe=>{

    cards.innerHTML += `
      <div class="card">

        <span class="badge">${dupe.category}</span>

        <div class="title">${dupe.title}</div>

        <div class="desc">${dupe.description}</div>

        ${dupe.screenshot_url ? `
          <img class="preview" src="${dupe.screenshot_url}">
        ` : ''}

        <div class="meta">
          ${new Date(dupe.created_at).toLocaleString()}
        </div>

        <div class="actions">

          <a href="${dupe.dupe_url}" target="_blank">
            <button class="tiny">Download</button>
          </a>

          <button class="tiny delete" onclick="deleteDupe(${dupe.id})">
            Delete
          </button>

        </div>

      </div>
    `;

  });
}

loadDupes();

</script>

</body>
</html>
