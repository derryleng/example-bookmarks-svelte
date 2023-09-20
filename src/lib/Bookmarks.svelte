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
  $: selected = bookmarks[i];
  $: getSelection(selected);

  function addBookmark() {
    if (newBookmark.url) {
      bookmarks = bookmarks.concat(newBookmark);
      i = bookmarks.length - 1; // Select newest bookmark
      newBookmark = { title: "", url: "" };
    }
  }

  function editBookmark() {
    if (selected && newBookmark.url) {
      selected.title = newBookmark.title;
      selected.url = newBookmark.url;
      bookmarks = bookmarks;
    }
  }

  function removeBookmark() {
    if (selected) {
      bookmarks = bookmarks.filter(item => item != selected);
      i = Math.min(i, bookmarks.length - 1); // Make sure selection is never lost
      newBookmark = { title: "", url: "" };
    }
  }

  function getSelection(x) {
    if (x) {
      newBookmark.title = x.title;
      newBookmark.url = x.url;
    } else {
      // When last bookmark is removed, x is undefined
      newBookmark = { title: "", url: "" }
    }
  }

  function moveUp() {
    const index = bookmarks.indexOf(selected);
    if (index > 0) {
      bookmarks = [...bookmarks.slice(0, index - 1), bookmarks[index], bookmarks[index - 1], ...bookmarks.slice(index + 1)];
      i -= 1;
    }
  }

  function moveDown() {
    const index = bookmarks.indexOf(selected);
    if (index < bookmarks.length) {
      bookmarks = [...bookmarks.slice(0, index), bookmarks[index + 1], bookmarks[index], ...bookmarks.slice(index + 2)];
      i += 1;
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

<div class="card">
  <button on:click={addBookmark} disabled={!newBookmark.url}>Add</button>
  <button on:click={editBookmark} disabled={!newBookmark.url || !selected}>Edit</button>
  <button on:click={removeBookmark} disabled={!selected}>Remove</button>
</div>

<div class="card">
  <button on:click={moveUp} disabled={!selected || bookmarks.indexOf(selected) < 1}>Move Up</button>
  <button on:click={moveDown} disabled={!selected || bookmarks.indexOf(selected) > bookmarks.length - 2}>Move Down</button>
</div>
