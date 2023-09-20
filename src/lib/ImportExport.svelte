<script>
  function importBookmarks() {
    const inputElement = document.createElement('input');
    inputElement.type = 'file';
    inputElement.accept = '.html, .json';
    inputElement.click();

    inputElement.addEventListener('change', (event) => {
      const selectedFile = event.target.files[0];

      if (!selectedFile) {
        alert('No file selected.');
        return;
      }

      const fileType = selectedFile.type;

      if (fileType === 'text/html') {
        readHTMLFile(selectedFile);
      } else if (fileType === 'application/json') {
        readJSONFile(selectedFile);
      } else {
        alert('Unsupported file type. Please select an HTML file (for Chrome bookmarks) or JSON file (for Firefox bookmarks).');
      }
    });
  }

  function readHTMLFile(file) {
    const reader = new FileReader();

    reader.onload = function (event) {
      const htmlContent = event.target.result;
      // TODO: Process the HTML content here
      console.log('HTML content:', htmlContent);
    };

    reader.readAsText(file);
  }

  function readJSONFile(file) {
    const reader = new FileReader();

    reader.onload = function (event) {
      const jsonContent = JSON.parse(event.target.result);
      // TODO: Process the JSON content here
      console.log('JSON content:', jsonContent);
    };

    reader.readAsText(file);
  }

  function exportBookmarks() {
    // TODO
  }
</script>

<div class="card">
  <button on:click={importBookmarks}>Import</button>
  <button on:click={exportBookmarks}>Export</button>
</div>
