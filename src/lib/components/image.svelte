<script>
 export let file

  
function previewFile() {
  const preview = document.querySelector('img');
   file = document.querySelector('input[type=file]').files[0];
  const reader = new FileReader();

  reader.addEventListener("load", function () {
    // convert image file to base64 string
    preview.src = reader.result;
  }, false);

  if (file) {
    reader.readAsDataURL(file);
  }
}

</script>

<input type="file" on:change={previewFile}><br>
<img  src="" height="200" alt="Image preview..." >
 
<slot  file={file} ></slot>

 
 