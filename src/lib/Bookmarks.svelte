<script>

  let newBookmark = { title: "", url: "" };
  let i = 0;

  $: bookmarks = [
    { title: "Apple", url: "www.apple.com" },
    { title: "Google", url: "www.google.com" },
    { title: "Facebook", url: "www.facebook.com" },
    { title: "Amazon", url: "www.amazon.com" },
    { title: "Tesla", url: "www.tesla.com" },
    { title: "Microsoft", url: "www.microsoft.com" },
    { title: "LinkedIn", url: "www.linkedin.com" },
  ];

  function addBookmark() {
    if (newBookmark.url != "") {
      bookmarks = bookmarks.concat(newBookmark);
      newBookmark = { title: "", url: "" };
    }
  }

  function editBookmark() {

  }

  function removeBookmark() {

  }

</script>

<div class="bookmark-container">
  {#each bookmarks as bookmark, i}
    <div class="bookmark">
      <h2>{bookmark.title}</h2>
      <p>{bookmark.url}</p>
    </div>
  {/each}
</div>

<input bind:value={newBookmark.title} placeholder="Title" />
<input bind:value={newBookmark.url} placeholder="URL" />

<button on:click={addBookmark} disabled={!newBookmark.url}>Add</button>
<button on:click={editBookmark}>Edit</button>
<button on:click={removeBookmark}>Remove</button>
