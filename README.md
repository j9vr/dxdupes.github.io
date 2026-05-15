E html>
</div>

<script>

const WEBHOOK = 'https://discord.com/api/webhooks/1504773551012712518/k6_GNEOlwjg0KrUS58l-XdwkLl8vpzHHRBArVzHiptq5hAVqT4B7C9SC8OrOMKYx5-kq';

async function sendDupe(){

  const title = document.getElementById('title').value;
  const description = document.getElementById('description').value;
  const download = document.getElementById('download').value;
  const image = document.getElementById('image').value;

  if(!title || !description || !download){
    alert('Fill everything');
    return;
  }

  const payload = {

    embeds:[
      {
        title:title,
        description:description,
        color:10181046,

        fields:[
          {
            name:'Download',
            value:`[Click Here](${download})`
          }
        ],

        image:{
          url:image
        }
      }
    ]
  };

  const response = await fetch(WEBHOOK,{
    method:'POST',
    headers:{
      'Content-Type':'application/json'
    },
    body:JSON.stringify(payload)
  });

  if(response.ok){

    alert('Dupe posted to Discord!');

    document.getElementById('title').value='';
    document.getElementById('description').value='';
    document.getElementById('download').value='';
    document.getElementById('image').value='';

  }else{
    alert('Webhook failed');
  }
}

</script>

</body>
</html>
