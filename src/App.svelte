<script lang="ts">
  import { RuleCMSWidget, RuleCMSWidgetProvider } from '@rulecms/widget-svelte';
  import * as sourceComponents from '@rulecms/source-components-svelte';
  import { DEMO_PUBLISHED_KEY, DEMO_RULECMS_TOKEN } from './rulecms-config';

  const title = 'RuleCMS Widget Demo';
  const token = DEMO_RULECMS_TOKEN;
  const publishedKey = DEMO_PUBLISHED_KEY;
  /**
   * Required since @rulecms/widget-svelte does not ship a concrete library.
   * Register the default Svelte source components here.
   */
  const libraries = { default: sourceComponents };
</script>

<RuleCMSWidgetProvider {token} {libraries}>
  <div class="app">
    <header class="app-header">
      <h1>{title}</h1>
      <p class="app-description">
        This is a demonstration of how to integrate RuleCMS widgets into a Svelte
        application
      </p>
    </header>

    <main class="app-main">
      <section class="widget-demo-section">
        <h2>Demo RuleCMS Widget</h2>
        <p>
          The widget below is rendered using the
          <code>RuleCMSWidget</code> component from the
          <code>@rulecms/widget-svelte</code> package, with
          <code>@rulecms/source-components-svelte</code> registered as the
          default component library.
        </p>

        <div class="info-card">
          <div class="info-card-content">
            <strong>Getting Started</strong>
            <p>
              If you are seeing an error below, replace the demo published key
              and app token in
              <code>src/rulecms-config.ts</code>
              with values from your
              <a
                href="https://rulecms.com"
                target="_blank"
                rel="noopener noreferrer"
              >RuleCMS.com</a>
              account.
            </p>
          </div>
        </div>

        <div class="widget-container">
          <RuleCMSWidget {publishedKey} />
        </div>
      </section>

      <section class="integration-info">
        <h2>Integration Steps</h2>
        <ol>
          <li>
            Install the packages:
            <code>npm install @rulecms/widget-svelte @rulecms/source-components-svelte</code>
          </li>
          <li>
            Wrap your app with
            <code>RuleCMSWidgetProvider</code>
            and register
            <code>{'{ default: sourceComponents }'}</code>
          </li>
          <li>
            Add
            <code>RuleCMSWidget</code>
            with your published key
          </li>
          <li>That is it. Your widget is now integrated and ready to display</li>
        </ol>
      </section>

      <section class="next-steps">
        <h2>Next Steps</h2>
        <ul>
          <li>
            Replace the demo published key with your actual widget published key
          </li>
          <li>Set your app token in <code>src/rulecms-config.ts</code></li>
          <li>Create and publish more widgets in the RuleCMS composer</li>
          <li>Explore RuleCMS widgets in your own Svelte applications</li>
        </ul>
      </section>
    </main>

    <footer class="app-footer">
      <p>
        Built with <span class="heart">❤️</span> using
        <a href="https://rulecms.com" target="_blank" rel="noopener noreferrer">RuleCMS</a>
        and Svelte
      </p>
    </footer>
  </div>
</RuleCMSWidgetProvider>

<style>
  .app {
    text-align: center;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }

  .app-header {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    padding: 3rem 2rem;
    color: white;
  }

  .app-header h1 {
    margin: 0;
    font-size: 2.5rem;
    font-weight: 700;
  }

  .app-description {
    margin: 1rem auto 0;
    font-size: 1.1rem;
    opacity: 0.9;
    max-width: 600px;
  }

  .app-main {
    flex: 1;
    padding: 2rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .widget-demo-section {
    margin-bottom: 3rem;
  }

  .widget-demo-section h2 {
    color: #333;
    margin-bottom: 1rem;
  }

  .widget-demo-section a {
    color: #667eea;
    text-decoration: none;
    font-weight: 600;
  }

  .widget-demo-section a:hover {
    color: #764ba2;
    text-decoration: underline;
  }

  .info-card {
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
    border: 1px solid rgba(102, 126, 234, 0.1);
    border-radius: 12px;
    padding: 1.5rem;
    margin: 1.5rem 0;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.07), 0 1px 3px rgba(0, 0, 0, 0.06);
  }

  .info-card-content {
    width: 100%;
  }

  .info-card-content strong {
    display: block;
    color: #2c3e50;
    font-size: 1.1rem;
    margin-bottom: 0.5rem;
  }

  .info-card-content p {
    margin: 0;
    color: #495057;
    line-height: 1.6;
  }

  .widget-container {
    background: #f8f9fa;
    border: 2px dashed #dee2e6;
    border-radius: 8px;
    padding: 2rem;
    margin: 2rem 0;
    min-height: 200px;
  }

  .integration-info,
  .next-steps {
    background: white;
    border: 1px solid #e9ecef;
    border-radius: 8px;
    padding: 2rem;
    margin: 2rem 0;
    text-align: left;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .integration-info h2,
  .next-steps h2 {
    color: #495057;
    margin-top: 0;
    margin-bottom: 1rem;
  }

  .integration-info ol,
  .next-steps ul {
    padding-left: 1.5rem;
  }

  .integration-info li,
  .next-steps li {
    margin-bottom: 0.5rem;
    line-height: 1.6;
  }

  code {
    background: #f1f3f4;
    padding: 0.2em 0.4em;
    border-radius: 3px;
    font-size: 0.9em;
    color: #d73a49;
  }

  .app-footer {
    background: #f8f9fa;
    padding: 2rem;
    border-top: 1px solid #e9ecef;
    margin-top: auto;
  }

  .app-footer a {
    color: #667eea;
    text-decoration: none;
    font-weight: 600;
  }

  .app-footer a:hover {
    color: #764ba2;
    text-decoration: underline;
  }

  .heart {
    color: #e74c3c;
  }

  @media (max-width: 768px) {
    .app-header {
      padding: 2rem 1rem;
    }

    .app-header h1 {
      font-size: 2rem;
    }

    .app-main {
      padding: 1rem;
    }

    .integration-info,
    .next-steps {
      padding: 1.5rem;
    }
  }
</style>
