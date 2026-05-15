<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>DXDupes Online</title>

  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #0b1020;
      color: white;
      padding: 20px;
    }

    h1 {
      color: #9b5cff;
    }

    .box {
      background: #131933;
      border-radius: 14px;
      padding: 20px;
      margin-bottom: 20px;
    }

    input, textarea {
      width: 100%;
      padding: 12px;
      margin-top: 10px;
      margin-bottom: 10px;
      border-radius: 10px;
      border: none;
      background: #1a2142;
      color: white;
    }

    button {
      background: #7c4dff;
      color: white;
      border: none;
      padding: 12px 18px;
      border-radius: 10px;
      cursor: pointer;
      font-weight: bold;
    }

    .dupe {
      background: #151c38;
      padding: 15px;
      border-radius: 14px;
      margin-bottom: 15px;
    }

    img {
      width: 100%;
      max-width: 400px;
      border-radius: 12px;
      margin-top: 10px;
    }

    a {
      color: #9b5cff;
    }
  </style>
</head>
<body>

  <h1>DXDupes</h1>

  <div class="box">
    <h2>Upload Dupe</h2>

    <input id="title" placeholder="Dupe title">

    <textarea id="description" placeholder="Description"></textarea>

    <input type="file" id="dupeFile">

    <input type="file" id="screenshotFile" accept="image/*">

    <button onclick="uploadDupe()">Post Dupe</button>
  </div>

  <div id="dupes"></div>

<script>

const SUPABASE_URL = 'PASTE_YOUR_SUPABASE_URL';
const SUPABASE_KEY = 'PASTE_YOUR_SUPABASE_ANON_KEY';

const supabaseClient = supabase.createClient(SUPABASE_URL, SUPABASE_KEY);

async function uploadDupe() {

  const title = document.getElementById('title').value;
  const description = document.getElementById('description').value;

  const dupeFile = document.getElementById('dupeFile').files[0];
  const screenshotFile = document.getElementById('screenshotFile').files[0];

  if (!title || !description || !dupeFile) {
    alert('Fill everything');
    return;
  }

  const dupePath = `dupes/${Date.now()}_${dupeFile.name}`;

  const { error: dupeError } = await supabaseClient
    .storage
    .from('files')
    .upload(dupePath, dupeFile);

  if (dupeError) {
    alert(dupeError.message);
    return;
  }

  const dupeUrl = supabaseClient
    .storage
    .from('files')
    .getPublicUrl(dupePath)
    .data.publicUrl;

  let screenshotUrl = '';

  if (screenshotFile) {

    const screenshotPath = `screenshots/${Date.now()}_${screenshotFile.name}`;

    const { error: screenshotError } = await supabaseClient
      .storage
      .from('files')
      .upload(screenshotPath, screenshotFile);

    if (!screenshotError) {

      screenshotUrl = supabaseClient
        .storage
        .from('files')
        .getPublicUrl(screenshotPath)
        .data.publicUrl;
    }
  }

  const { error } = await supabaseClient
    .from('dupes')
    .insert([
      {
        title,
        description,
        dupe_url: dupeUrl,
        screenshot_url: screenshotUrl
      }
    ]);

  if (error) {
    alert(error.message);
    return;
  }

  alert('Dupe uploaded!');

  document.getElementById('title').value = '';
  document.getElementById('description').value = '';
  document.getElementById('dupeFile').value = '';
  document.getElementById('screenshotFile').value = '';

  loadDupes();
}

async function loadDupes() {

  const { data, error } = await supabaseClient
    .from('dupes')
    .select('*')
    .order('id', { ascending: false });

  if (error) {
    console.error(error);
    return;
  }

  const container = document.getElementById('dupes');

  container.innerHTML = '';

  data.forEach(dupe => {

    container.innerHTML += `
      <div class="dupe">
        <h2>${dupe.title}</h2>

        <p>${dupe.description}</p>

        <a href="${dupe.dupe_url}" target="_blank">
          Download Dupe
        </a>

        ${dupe.screenshot_url ? `
          <br>
          <img src="${dupe.screenshot_url}">
        ` : ''}
      </div>
    `;
  });
}

loadDupes();

</script>

</body>
</html>
