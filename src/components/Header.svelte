<style>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: var(--color-primary);
    color: var(--color-secondary);
    padding: 10px 20px;
    box-shadow: 0px 1px 3px 0px rgba(255, 255, 255, 1);
    position: sticky;
  }
  header .logo {
    display: flex;
    flex-flow: column;
    width: 360px;
    color: var(--color-secondary);
  }

  header .logo .title {
    font-size: 1.2rem;
    text-transform: uppercase;
    font-weight: bold;
  }
  header .logo .sub-title {
    font-size: 0.8rem;
  }
</style>

<header>
  <div class="logo">
    <span class="title">The Movie Database (TMDb)</span>
    <span class="sub-title">Is a community built movie and TV database.</span>
  </div>
</header>
