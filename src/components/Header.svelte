<style>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    background-color: #010101;
    color: var(--color-white);
    padding: 1.2rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    position: fixed;
    z-index: 9;
  }
  header .logo {
    display: flex;
    flex-flow: column;
    width: 360px;
  }

  header .logo .title {
    font-size: 1.2rem;
    text-transform: uppercase;
    font-weight: bold;
  }
  header .logo .sub-title {
    font-size: 0.9rem;
    font-weight: 500;
  }
</style>

<header>
  <div class="logo">
    <span class="title">The Movie Database (TMDb)</span>
    <span class="sub-title">Is a community built movie and TV database.</span>
  </div>
</header>
