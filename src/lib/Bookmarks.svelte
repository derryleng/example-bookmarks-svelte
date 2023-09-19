<script>

  let newBookmark = { title: "", url: "" };
  $: i = 0;

  $: bookmarks = [
    { title: "Apple", url: "www.apple.com" },
    { title: "Google", url: "www.google.com" },
    { title: "Facebook", url: "www.facebook.com" },
    { title: "Amazon", url: "www.amazon.com" },
    { title: "Tesla", url: "www.tesla.com" },
    { title: "Microsoft", url: "www.microsoft.com" },
    { title: "LinkedIn", url: "www.linkedin.com" },
  ];
  $: selected = bookmarks[i];
  $: getSelection(selected);

  function addBookmark() {
    bookmarks = bookmarks.concat(newBookmark);
    i = bookmarks.length - 1; // Select newest bookmark
    newBookmark = { title: "", url: "" };
  }

  function editBookmark() {
    selected.title = newBookmark.title;
    selected.url = newBookmark.url;
    bookmarks = bookmarks;
  }

  function removeBookmark() {
    bookmarks = bookmarks.filter(item => item != selected);
    i = Math.min(i, bookmarks.length - 1); // Make sure selection is never lost
    newBookmark = { title: "", url: "" };
  }

  function getSelection(x) {
    if (x) {
      newBookmark.title = x.title;
      newBookmark.url = x.url;
    } else {
      newBookmark = { title: "", url: "" }
    }
  }

</script>

<select bind:value={i} size={12}>
	{#each bookmarks as bookmark, i}
		<option value={i}>{i}, {bookmark.title}, {bookmark.url}</option>
	{/each}
</select>

<input bind:value={newBookmark.title} placeholder="Title" />
<input bind:value={newBookmark.url} placeholder="URL" />

<button on:click={addBookmark} disabled={!newBookmark.url}>Add</button>
<button on:click={editBookmark} disabled={!newBookmark.url || !selected}>Edit</button>
<button on:click={removeBookmark} disabled={!selected}>Remove</button>
