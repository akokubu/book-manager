<script>
  import NavElement from "./NavElement.svelte";
  import { fade } from "svelte/transition";
  import { fly } from "svelte/transition";

  let books = [
    {
      id: 1,
      name: "ゼロから始めるデザインシステム",
      imgUrl: "https://i.gyazo.com/a3ddad4c037aca4778628c826a64ce4c.jpg",
      author: "榊原宏祐 原田佳樹"
    },
    {
      id: 2,
      name: "アスキーアート技術読本",
      imgUrl: "https://i.gyazo.com/3992e2f40adb6706f9f187fe3c8843d4.jpg",
      author: "榊原宏祐"
    },
    {
      id: 3,
      name: "ポモドーロ GTD すきま時間予定表で目標達成する本",
      imgUrl: "https://i.gyazo.com/0e69af4e7fd229fae9c6b6c44c9bb4d9.png",
      author: "榊原宏祐"
    },
    {
      id: 4,
      name: "Nuxt Svelte Ionicで作る爆速フロントエンド 3つの世界",
      imgUrl: "https://i.gyazo.com/a5db257b7b48210536d387ba9ad5da80.jpg",
      author: "榊原宏祐 高橋拓也 中野伸吾"
    }
  ];

  let showedBook = books[0];
  let visible = true;
  let clickable = true;

  function navClicked(event) {
    if (clickable) {
      visible = false;
      clickable = false;
      showedBook = event.detail.book;
    }
  }
</script>

<style type="text/scss">
  main {
    margin: 0 auto;
    max-width: 960px;
  }
  .title {
    margin-left: 1em;
  }
  .nav-tab {
    .nav-tab-list {
      background-color: #333333;
      list-style-type: none;
      display: flex;
      justify-content: center;
      margin-bottom: 0;
      .nav-tab-list-el {
        min-width: 100px;
        margin: 16px 16px 0;
        opacity: 0.5;
        &.active {
          opacity: 1;
        }
        .book-thumb {
          height: 100px;
        }
      }
    }
  }
  .book {
    .book-container {
      height: 400px;
      display: flex;
      justify-content: center;
      background-size: 500px auto;
      background-position: center;
      padding: 32px 32px 32px 0;
      position: relative;
      z-index: 0;
      overflow: hidden;
      &::before {
        background: inherit;
        content: "";
        filter: blur(10px);
        position: absolute;
        top: -5px;
        right: -5px;
        bottom: -5px;
        left: -5px;
        z-index: -1;
      }
      .book-info {
        text-align: right;
        .label {
          display: inline-block;
          overflow-wrap: break-word;
          background-color: #333333;
          color: #f0f0f0;
          padding: 0 10px;
          border-radius: 4px;
          margin: 0 12px 12px 0;
          font-size: 24px;
        }
      }
      .book-img {
        height: 100%;
      }
      .shadowed {
        box-shadow: 10px 10px 60px 10px rgba(0, 0, 0, 0.4);
      }
    }
  }
</style>

<main>
  {#if visible}
    <section class="book">
      <div
        class="book-container"
        style={`background-image: url(${showedBook.imgUrl})};`}
        on:outroend={() => (visible = true)}
        on:introend={() => (clickable = true)}
        in:fly={{ y: 500, duration: 200 }}
        out:fade>
        <div class="book-info">
          <div class="lable showed">{showedBook.name}</div>
          <div class="lable shadowed">{showedBook.author}</div>
        </div>
        <img class="book-img" src={showedBook.imgUrl} />
      </div>
    </section>
  {/if}
  <nav class="nav-tab">
    <ul class="nav-tab-list">
      {#each books as book (book.id)}
        <NavElement
          active={book === showedBook}
          {book}
          on:navClicked={navClicked} />
      {/each}
    </ul>
  </nav>
</main>
