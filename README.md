<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="artifact-type" content="narrative">
  <meta name="design-style" content="carbon">
  <title>爆炸地震學：近地表爆炸事件之地面最大速度（PGV）衰減關係研究 — 演講紀錄與心得</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@300;400;500;600&family=IBM+Plex+Sans:wght@300;400;500;600;700&family=Noto+Sans+TC:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      color-scheme: light;

      /* 1. Carbon style tokens */
      --background: #ffffff;
      --surface-container-low: #f4f4f4;
      --surface-container: #f4f4f4;
      --surface-container-high: #e0e0e0;

      --on-surface: #161616;
      --on-surface-variant: #525252;

      --outline: #8d8d8d;
      --outline-variant: #e0e0e0;

      --primary: #0f62fe;
      --on-primary: #ffffff;
      --primary-hover: #0353e9;
      --primary-container: #d0e2ff;
      --on-primary-container: #161616;
      --secondary: #6f6f6f;
      --tertiary: #198038;
      --error: #da1e28;
      --on-error: #ffffff;

      --data-1: #0f62fe;
      --data-2: #6929c4;
      --data-3: #005d5d;
      --data-4: #9f1853;
      --data-context: #8d8d8d;

      --primary-tint: color-mix(in srgb, var(--primary) 12%, transparent);
      --data-2-tint: color-mix(in srgb, var(--data-2) 12%, transparent);
      --tertiary-tint: color-mix(in srgb, var(--tertiary) 10%, transparent);
      --error-tint: color-mix(in srgb, var(--error) 10%, transparent);

      --font-headline: 'Noto Sans TC', 'IBM Plex Sans', sans-serif;
      --font-body: 'Noto Sans TC', 'IBM Plex Sans', sans-serif;
      --font-label: 'IBM Plex Mono', 'Noto Sans TC', monospace;

      --rounded: 0.125rem;
      --rounded-lg: 0.25rem;
      --rounded-full: 0.75rem;

      --shadow-1: 0 2px 6px rgb(0 0 0 / 0.1);
      --shadow-2: 0 4px 12px rgb(0 0 0 / 0.12);
      --rule: 1px solid var(--outline-variant);
      --field-rule: 1px solid var(--outline);
      --indicator: 2px solid var(--primary);

      /* 2. Shared foundation tokens */
      --positive: #198038;
      --warning: #8a5a00;
      --focus: var(--primary);

      /* Narrative type scale tailored for Traditional Chinese + IBM Plex */
      --display-size: clamp(2rem, 1.35rem + 2.4vw, 3.125rem);
      --headline-size: clamp(1.5rem, 1.2rem + 1vw, 2rem);
      --subhead-size: clamp(1.125rem, 1.02rem + 0.4vw, 1.3125rem);
      --body-size: clamp(1rem, 0.96rem + 0.18vw, 1.0625rem);
      --label-size: 0.75rem;

      /* Spacing scale (4pt base) */
      --space-xs: 0.25rem;
      --space-sm: 0.5rem;
      --space-md: 1rem;
      --space-lg: 1.5rem;
      --space-xl: 2.5rem;
      --space-2xl: 4rem;
      --space-3xl: 6rem;

      /* Motion */
      --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
      --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
      --dur-micro: 120ms;
      --dur-short: 220ms;
      --dur-long: 420ms;
    }

    /* Base reset */
    *, *::before, *::after { box-sizing: border-box; }
    html, body { overflow-x: clip; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    header { position: static !important; }

    body {
      background: var(--background);
      color: var(--on-surface);
      font-family: var(--font-body);
      font-size: var(--body-size);
      line-height: 1.65;
      -webkit-font-smoothing: antialiased;
    }

    button, input, select, textarea {
      font-family: inherit;
    }

    a {
      color: var(--primary);
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
      text-underline-offset: 3px;
    }

    :focus-visible {
      outline: 2px solid var(--focus);
      outline-offset: 2px;
    }

    /* GitHub Pages top bar (non-sticky, clean repository/doc banner) */
    .repo-bar {
      border-bottom: var(--rule);
      background: var(--surface-container);
    }
    .repo-bar-inner {
      max-width: 1200px;
      margin: 0 auto;
      padding: var(--space-sm) var(--space-lg);
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: var(--space-sm);
    }
    .repo-path {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--on-surface-variant);
      display: flex;
      align-items: center;
      gap: var(--space-xs);
    }
    .repo-path strong {
      color: var(--on-surface);
      font-weight: 600;
    }
    .repo-tags {
      display: flex;
      flex-wrap: wrap;
      gap: var(--space-xs);
    }

    .tag {
      display: inline-flex;
      align-items: center;
      height: 24px;
      padding: 0 var(--space-sm);
      background: var(--primary-container);
      color: var(--on-primary-container);
      border-radius: var(--rounded-full);
      font-size: var(--label-size);
      font-weight: 400;
      line-height: 1;
      white-space: nowrap;
    }
    .tag-neutral {
      background: var(--surface-container-high);
      color: var(--on-surface);
    }

    /* Page Hero Header */
    .doc-header {
      border-bottom: var(--rule);
      background: var(--background);
    }
    .doc-header-inner {
      max-width: 1200px;
      margin: 0 auto;
      padding: var(--space-2xl) var(--space-lg) var(--space-xl);
    }
    .kicker {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--on-surface-variant);
      letter-spacing: 0.08em;
      text-transform: uppercase;
      margin: 0 0 var(--space-sm);
    }
    .headline-display {
      font-family: var(--font-headline);
      font-size: var(--display-size);
      font-weight: 300;
      line-height: 1.2;
      letter-spacing: 0;
      margin: 0 0 var(--space-md);
      max-width: 30ch;
    }
    .headline-display strong {
      font-weight: 600;
    }
    .doc-subtitle {
      font-size: var(--subhead-size);
      color: var(--on-surface-variant);
      max-width: 65ch;
      margin: 0 0 var(--space-lg);
      line-height: 1.55;
    }
    .meta-strip {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(min(180px, 100%), 1fr));
      gap: var(--space-md);
      padding-top: var(--space-md);
      border-top: var(--rule);
    }
    .meta-item {
      display: flex;
      flex-direction: column;
      gap: var(--space-xs);
    }
    .meta-label {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--on-surface-variant);
    }
    .meta-label-en {
      text-transform: uppercase;
      letter-spacing: 0.08em;
    }
    .meta-value {
      font-size: 0.9375rem;
      font-weight: 500;
      color: var(--on-surface);
    }

    /* Mobile quick-jump bar (visible below 860px) */
    .mobile-toc {
      display: none;
      border-bottom: var(--rule);
      background: var(--surface-container);
      padding: var(--space-sm) var(--space-lg);
      overflow-x: auto;
      gap: var(--space-sm);
    }
    .mobile-toc a {
      font-size: var(--label-size);
      color: var(--on-surface-variant);
      white-space: nowrap;
      padding: var(--space-xs) var(--space-sm);
      min-height: 36px;
      display: inline-flex;
      align-items: center;
      border-bottom: 2px solid transparent;
    }
    .mobile-toc a.is-active {
      color: var(--on-surface);
      font-weight: 600;
      border-bottom: var(--indicator);
    }

    /* Main Asymmetric Page Grid */
    .page-grid {
      display: grid;
      grid-template-columns: 240px minmax(0, 1fr);
      gap: var(--space-2xl);
      padding: var(--space-xl) var(--space-lg) var(--space-3xl);
      max-width: 1200px;
      margin: 0 auto;
      overflow: visible;
    }
    .page-grid * { min-width: 0; }

    /* Left Documentation Index */
    .side-column {
      align-self: start;
    }
    .side-nav {
      position: sticky;
      top: var(--space-lg);
      border-left: var(--rule);
    }
    .side-nav-title {
      font-family: var(--font-label);
      font-size: var(--label-size);
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--on-surface-variant);
      padding: 0 0 var(--space-sm) var(--space-md);
      margin: 0;
    }
    .side-nav-list {
      list-style: none;
      margin: 0;
      padding: 0;
    }
    .side-nav-list a {
      display: flex;
      align-items: baseline;
      gap: var(--space-sm);
      padding: var(--space-sm) var(--space-md);
      font-size: 0.875rem;
      color: var(--on-surface-variant);
      border-left: 2px solid transparent;
      margin-left: -1px;
      transition: color var(--dur-micro) var(--ease-out), background-color var(--dur-micro) var(--ease-out);
    }
    .side-nav-list a:hover {
      background: var(--surface-container);
      color: var(--on-surface);
      text-decoration: none;
    }
    .side-nav-list a.is-active {
      border-left: var(--indicator);
      color: var(--on-surface);
      font-weight: 600;
      background: var(--surface-container);
    }
    .nav-idx {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--on-surface-variant);
      flex-shrink: 0;
    }

    /* Main Content Column */
    .main-column {
      display: flex;
      flex-direction: column;
      gap: var(--space-2xl);
    }

    .doc-section {
      scroll-margin-top: var(--space-lg);
    }

    .section-head {
      border-bottom: var(--rule);
      padding-bottom: var(--space-sm);
      margin-bottom: var(--space-lg);
    }
    .section-code {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--primary);
      letter-spacing: 0.08em;
      text-transform: uppercase;
      display: block;
      margin-bottom: var(--space-xs);
    }
    .section-title {
      font-family: var(--font-headline);
      font-size: var(--headline-size);
      font-weight: 300;
      line-height: 1.25;
      margin: 0;
    }
    .section-title strong {
      font-weight: 600;
    }

    .prose {
      max-width: 65ch;
      margin: 0 0 var(--space-md);
      color: var(--on-surface);
    }
    .prose-muted {
      max-width: 65ch;
      margin: 0 0 var(--space-md);
      color: var(--on-surface-variant);
    }

    /* Carbon Flat Gray Layers & Metric Tiles */
    .layer {
      background: var(--surface-container);
      border-radius: 0;
      padding: var(--space-md);
    }
    .layer .layer {
      background: var(--surface-container-high);
    }

    .kpi-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(min(200px, 100%), 1fr));
      gap: var(--space-md);
      margin-bottom: var(--space-lg);
    }
    .kpi-tile {
      background: var(--surface-container);
      padding: var(--space-md);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      gap: var(--space-sm);
    }
    .kpi-tile.is-primary {
      border-bottom: var(--indicator);
    }
    .kpi-label {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--on-surface-variant);
    }
    .kpi-value {
      font-family: var(--font-label);
      font-weight: 300;
      font-size: clamp(1.5rem, 1.2rem + 1vw, 2rem);
      line-height: 1.15;
      color: var(--on-surface);
      font-variant-numeric: tabular-nums;
    }
    .kpi-helper {
      font-size: 0.8125rem;
      color: var(--on-surface-variant);
      line-height: 1.45;
    }

    /* Carbon Callout / Notification strip */
    .callout {
      background: var(--surface-container);
      border-left: 3px solid var(--primary);
      padding: var(--space-md) var(--space-lg);
      margin: var(--space-lg) 0;
    }
    .callout-positive {
      border-left-color: var(--tertiary);
    }
    .callout-warning {
      border-left-color: var(--warning);
    }
    .callout-title {
      font-weight: 600;
      font-size: 0.9375rem;
      margin: 0 0 var(--space-xs);
      color: var(--on-surface);
    }
    .callout p {
      margin: 0;
      font-size: 0.9375rem;
      color: var(--on-surface-variant);
      max-width: 65ch;
    }

    /* Adaptive 2D Card Grid */
    .card-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(min(280px, 100%), 1fr));
      gap: var(--space-md);
      margin: var(--space-md) 0;
    }
    .card-tile {
      background: var(--surface-container);
      padding: var(--space-lg);
      display: flex;
      flex-direction: column;
      gap: var(--space-sm);
    }
    .card-tile-head {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      gap: var(--space-sm);
      border-bottom: var(--rule);
      padding-bottom: var(--space-sm);
    }
    .card-tile-title {
      font-weight: 600;
      font-size: 1.0625rem;
      margin: 0;
    }
    .card-tile-code {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--on-surface-variant);
      text-transform: uppercase;
      letter-spacing: 0.08em;
    }

    /* Carbon Tables */
    .table-wrap {
      width: 100%;
      overflow-x: auto;
      margin: var(--space-md) 0 var(--space-lg);
    }
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.9375rem;
      text-align: left;
    }
    thead tr {
      background: var(--surface-container-high);
      border-bottom: var(--rule);
    }
    th {
      font-family: var(--font-label);
      font-size: var(--label-size);
      font-weight: 600;
      color: var(--on-surface);
      padding: var(--space-sm) var(--space-md);
      white-space: nowrap;
    }
    td {
      padding: var(--space-sm) var(--space-md);
      border-bottom: var(--rule);
      vertical-align: top;
      color: var(--on-surface);
    }
    tbody tr:nth-child(even) {
      background: var(--surface-container);
    }
    .td-mono {
      font-family: var(--font-label);
      font-size: 0.875rem;
      font-variant-numeric: tabular-nums;
    }

    /* Interactive Tabs (Carbon underline bar) */
    .tab-bar {
      display: flex;
      flex-wrap: wrap;
      border-bottom: var(--rule);
      gap: var(--space-xs);
      margin-bottom: var(--space-md);
    }
    .tab-btn {
      background: transparent;
      border: 0;
      border-bottom: 2px solid transparent;
      padding: var(--space-sm) var(--space-md);
      min-height: 44px;
      font-size: 0.9375rem;
      font-weight: 400;
      color: var(--on-surface-variant);
      cursor: pointer;
      transition: color var(--dur-micro) var(--ease-out), background-color var(--dur-micro) var(--ease-out);
    }
    .tab-btn:hover {
      background: var(--surface-container);
      color: var(--on-surface);
    }
    .tab-btn.is-active {
      color: var(--on-surface);
      font-weight: 600;
      border-bottom: var(--indicator);
    }

    .tab-panel {
      display: none;
    }
    .tab-panel.is-active {
      display: block;
    }

    /* Carbon Buttons & Controls */
    .control-row {
      display: flex;
      flex-wrap: wrap;
      align-items: end;
      gap: var(--space-md);
      margin-bottom: var(--space-md);
    }
    .control-group {
      display: flex;
      flex-direction: column;
      gap: var(--space-xs);
      min-width: 180px;
    }
    .control-label {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--on-surface-variant);
    }
    .btn-group {
      display: flex;
      flex-wrap: wrap;
      gap: var(--space-xs);
    }
    .btn {
      min-height: 44px;
      padding: var(--space-sm) var(--space-md);
      border-radius: 0;
      font-size: 0.875rem;
      font-weight: 500;
      cursor: pointer;
      border: 1px solid var(--primary);
      background: var(--background);
      color: var(--primary);
      transition: background-color var(--dur-micro) var(--ease-out), color var(--dur-micro) var(--ease-out);
    }
    .btn:hover {
      background: var(--surface-container);
    }
    .btn.is-selected,
    .btn-primary {
      background: var(--primary);
      color: var(--on-primary);
      border-color: var(--primary);
    }
    .btn-primary:hover,
    .btn.is-selected:hover {
      background: var(--primary-hover);
    }

    input[type="range"] {
      width: 100%;
      accent-color: var(--primary);
      min-height: 40px;
      cursor: pointer;
    }

    /* Interactive Figure Frame */
    .figure-box {
      background: var(--surface-container);
      padding: var(--space-lg);
      margin: var(--space-md) 0;
    }
    .figure-header {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: baseline;
      gap: var(--space-sm);
      margin-bottom: var(--space-md);
    }
    .figure-title {
      font-size: 1.0625rem;
      font-weight: 600;
      margin: 0;
    }
    .figure-units {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--on-surface-variant);
    }
    .legend-row {
      display: flex;
      flex-wrap: wrap;
      gap: var(--space-md);
      margin-bottom: var(--space-sm);
      font-size: 0.8125rem;
      color: var(--on-surface-variant);
    }
    .legend-item {
      display: inline-flex;
      align-items: center;
      gap: var(--space-xs);
    }
    .swatch {
      width: 12px;
      height: 12px;
      display: inline-block;
      flex-shrink: 0;
    }
    .swatch-blue { background: var(--data-1); }
    .swatch-purple { background: var(--data-2); }
    .swatch-teal { background: var(--data-3); }
    .swatch-gray { background: var(--data-context); }

    .svg-stage {
      background: var(--background);
      border: var(--rule);
      padding: var(--space-md);
      min-height: 260px;
    }
    .svg-stage svg {
      width: 100%;
      height: auto;
      display: block;
    }
    .figure-caption {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--on-surface-variant);
      margin-top: var(--space-sm);
      line-height: 1.5;
    }

    /* Focal Sphere Dual Container */
    .focal-split {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(min(240px, 100%), 1fr));
      gap: var(--space-md);
    }
    .focal-card {
      background: var(--background);
      border: var(--rule);
      padding: var(--space-md);
    }
    .focal-readout {
      margin-top: var(--space-sm);
      padding: var(--space-sm) var(--space-md);
      background: var(--surface-container);
      font-family: var(--font-label);
      font-size: 0.8125rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    /* Pipeline List (TAIGER Steps) */
    .pipeline-list {
      list-style: none;
      padding: 0;
      margin: var(--space-md) 0;
      border-top: var(--rule);
    }
    .pipeline-item {
      display: grid;
      grid-template-columns: 72px minmax(0, 1fr);
      gap: var(--space-md);
      padding: var(--space-md) 0;
      border-bottom: var(--rule);
      align-items: start;
    }
    .pipeline-step {
      font-family: var(--font-label);
      font-size: var(--label-size);
      font-weight: 600;
      color: var(--primary);
      text-transform: uppercase;
      letter-spacing: 0.08em;
      padding-top: 2px;
    }
    .pipeline-body h3 {
      margin: 0 0 var(--space-xs);
      font-size: 1rem;
      font-weight: 600;
    }
    .pipeline-body p {
      margin: 0;
      font-size: 0.9375rem;
      color: var(--on-surface-variant);
      max-width: 65ch;
    }

    /* Interactive Case Readout Grid */
    .attenuation-readout {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(min(170px, 100%), 1fr));
      gap: var(--space-sm);
      margin-top: var(--space-md);
    }
    .readout-cell {
      background: var(--background);
      border: var(--rule);
      padding: var(--space-sm) var(--space-md);
    }
    .readout-cell .kpi-label {
      display: block;
      margin-bottom: var(--space-xs);
    }
    .readout-val {
      font-family: var(--font-label);
      font-size: 1.25rem;
      font-weight: 500;
      color: var(--on-surface);
      font-variant-numeric: tabular-nums;
    }
    .readout-val.is-alert {
      color: var(--error);
    }
    .readout-val.is-primary {
      color: var(--primary);
    }

    /* Reflection & Concept Check */
    .reflection-list > * + * {
      border-top: var(--rule);
      padding-top: var(--space-lg);
      margin-top: var(--space-lg);
    }
    .reflection-item h3 {
      font-size: 1.0625rem;
      font-weight: 600;
      margin: 0 0 var(--space-xs);
    }
    .reflection-item p {
      margin: 0;
      max-width: 65ch;
      color: var(--on-surface);
    }

    .quiz-card {
      background: var(--surface-container);
      padding: var(--space-lg);
      margin-top: var(--space-md);
    }
    .quiz-q {
      font-weight: 600;
      margin: 0 0 var(--space-md);
    }
    .quiz-options {
      display: flex;
      flex-direction: column;
      gap: var(--space-xs);
    }
    .quiz-opt {
      text-align: left;
      min-height: 44px;
      padding: var(--space-sm) var(--space-md);
      background: var(--background);
      border: 1px solid var(--outline-variant);
      color: var(--on-surface);
      font-size: 0.9375rem;
      cursor: pointer;
      transition: background-color var(--dur-micro) var(--ease-out);
    }
    .quiz-opt:hover {
      background: var(--surface-container-high);
    }
    .quiz-opt.is-chosen {
      background: var(--primary-container);
      color: var(--on-primary-container);
      border-color: var(--primary);
      font-weight: 500;
    }
    .quiz-feedback {
      margin-top: var(--space-sm);
      padding: var(--space-sm) var(--space-md);
      background: var(--background);
      border-left: 3px solid var(--primary);
      font-size: 0.875rem;
      color: var(--on-surface);
      display: none;
    }
    .quiz-feedback.is-visible {
      display: block;
    }
    .quiz-feedback.is-correct {
      border-left-color: var(--tertiary);
    }
    .quiz-feedback.is-wrong {
      border-left-color: var(--error);
    }

    /* Footer */
    .doc-footer {
      border-top: var(--rule);
      background: var(--surface-container);
      padding: var(--space-xl) var(--space-lg);
    }
    .doc-footer-inner {
      max-width: 1200px;
      margin: 0 auto;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: var(--space-md);
      font-size: 0.875rem;
      color: var(--on-surface-variant);
    }

    /* Scroll reveal */
    .reveal-block {
      opacity: 1;
      transform: translateY(0);
      transition: opacity var(--dur-short) var(--ease-out), transform var(--dur-short) var(--ease-out);
    }

    /* SVG shared styles (using tokens only) */
    .svg-grid { stroke: var(--outline-variant); stroke-width: 1; }
    .svg-axis { stroke: var(--outline); stroke-width: 1.5; }
    .svg-text { fill: var(--on-surface-variant); font-family: var(--font-label); font-size: 11px; }
    .svg-text-strong { fill: var(--on-surface); font-family: var(--font-label); font-size: 12px; font-weight: 600; }
    .svg-wave-primary { stroke: var(--data-1); stroke-width: 2; fill: none; }
    .svg-wave-compare { stroke: var(--data-2); stroke-width: 1.8; fill: none; }
    .svg-wave-context { stroke: var(--data-context); stroke-width: 1.2; fill: none; }

    /* Responsive adjustments */
    @media (max-width: 860px) {
      .page-grid {
        grid-template-columns: 1fr;
        gap: var(--space-lg);
      }
      .side-column {
        display: none;
      }
      .mobile-toc {
        display: flex;
      }
    }

    @media (max-width: 640px) {
      .page-grid { grid-template-columns: 1fr; padding: var(--space-md); }
      aside { display: none; }
      body { padding: 0; }
      .doc-header-inner { padding: var(--space-xl) var(--space-md) var(--space-lg); }
      .figure-box { padding: var(--space-md); }
      .pipeline-item { grid-template-columns: 1fr; gap: var(--space-xs); }
    }

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        animation-duration: 0.01ms !important;
        transition-duration: 0.01ms !important;
        scroll-behavior: auto !important;
      }
    }
  </style>
</head>
<body>

  <!-- GitHub Pages Repository Context Bar -->
  <div class="repo-bar">
    <div class="repo-bar-inner">
      <div class="repo-path">
        <span>seismology-notes</span>
        <span>/</span>
        <strong>explosion-pgv-attenuation</strong>
      </div>
      <div class="repo-tags">
        <span class="tag">爆炸地震學</span>
        <span class="tag tag-neutral">PGV 衰減關係</span>
        <span class="tag tag-neutral">演講紀錄與心得</span>
      </div>
    </div>
  </div>

  <!-- Document Header -->
  <header class="doc-header">
    <div class="doc-header-inner">
      <p class="kicker">Seminar Record &amp; Research Notes · Forensic Seismology</p>
      <h1 class="headline-display">
        爆炸地震學：<strong>近地表爆炸事件之地面最大速度（PGV）衰減關係研究</strong>
      </h1>
      <p class="doc-subtitle">
        從核試爆波形鑑別、TAIGER 計畫人工井穴爆破，到 2014 年高雄氣爆規模反推與台灣西部平原近場地動效應的系統性整理與演講反思。
      </p>
      <div class="meta-strip">
        <div class="meta-item">
          <span class="meta-label meta-label-en">SPEAKER / 主講人</span>
          <span class="meta-value">梁文宗 研究員</span>
        </div>
        <div class="meta-item">
          <span class="meta-label meta-label-en">KEY EXPERIMENT / 核心實驗</span>
          <span class="meta-value">TAIGER 計畫 10 次人工井穴爆破</span>
        </div>
        <div class="meta-item">
          <span class="meta-label meta-label-en">CASE STUDY / 實例應用</span>
          <span class="meta-value">2014 年高雄氣爆（推估 <i>M</i><sub>L</sub> 2.38）</span>
        </div>
        <div class="meta-item">
          <span class="meta-label meta-label-en">DATE / 整理日期</span>
          <span class="meta-value">2026-11-25</span>
        </div>
      </div>
    </div>
  </header>

  <!-- Mobile Section Quick-Jump -->
  <nav class="mobile-toc" aria-label="章節快速導覽">
    <a href="#sec-summary" class="is-active">01 演講摘要</a>
    <a href="#sec-forensic">02 法醫地震學</a>
    <a href="#sec-nuclear">03 核試爆波形特徵</a>
    <a href="#sec-taiger">04 TAIGER 炸測實驗</a>
    <a href="#sec-attenuation">05 PGV 衰減與南線異常</a>
    <a href="#sec-kaohsiung">06 高雄氣爆實例</a>
    <a href="#sec-reflection">07 專題心得與討論</a>
  </nav>

  <!-- Main Documentation Grid -->
  <div class="page-grid">

    <!-- Left Sticky Documentation Sidebar -->
    <aside class="side-column">
      <nav class="side-nav" aria-label="目錄導覽">
        <p class="side-nav-title">Contents · 目錄</p>
        <ul class="side-nav-list">
          <li><a href="#sec-summary" class="is-active"><span class="nav-idx">01</span><span>演講摘要</span></a></li>
          <li><a href="#sec-forensic"><span class="nav-idx">02</span><span>法醫地震學介紹</span></a></li>
          <li><a href="#sec-nuclear"><span class="nav-idx">03</span><span>核試爆波形特徵</span></a></li>
          <li><a href="#sec-taiger"><span class="nav-idx">04</span><span>TAIGER 炸測實驗</span></a></li>
          <li><a href="#sec-attenuation"><span class="nav-idx">05</span><span>PGV 衰減關係式擬合</span></a></li>
          <li><a href="#sec-kaohsiung"><span class="nav-idx">06</span><span>高雄氣爆實例應用</span></a></li>
          <li><a href="#sec-reflection"><span class="nav-idx">07</span><span>專題心得與討論</span></a></li>
        </ul>
      </nav>
    </aside>

    <!-- Main Reading & Interactive Column -->
    <main class="main-column">

      <!-- Section 01: 演講摘要 -->
      <section id="sec-summary" class="doc-section">
        <div class="section-head">
          <span class="section-code">01 · Executive Summary</span>
          <h2 class="section-title">演講摘要：<strong>當地震儀成為沒有目擊者時的客觀證詞</strong></h2>
        </div>

        <div class="kpi-grid">
          <div class="kpi-tile is-primary">
            <span class="kpi-label">TAIGER 人工井穴爆破</span>
            <span class="kpi-value">10 次</span>
            <span class="kpi-helper">時間、位置與炸藥量皆精確已知，彌補天然地震參數不確定性</span>
          </div>
          <div class="kpi-tile">
            <span class="kpi-label">高雄氣爆推估規模</span>
            <span class="kpi-value"><i>M</i><sub>L</sub> 2.38</span>
            <span class="kpi-helper">首度以近地表爆炸 PGV 衰減關係式反推之都市氣爆規模</span>
          </div>
          <div class="kpi-tile">
            <span class="kpi-label">震源鑑別雙指標</span>
            <span class="kpi-value"><i>m</i><sub>b</sub>/<i>M</i><sub>s</sub> &amp; <i>P</i><sub>g</sub>/<i>L</i><sub>g</sub></span>
            <span class="kpi-helper">結合球形膨脹分量，精準區分地下核試爆與天然構造地震</span>
          </div>
          <div class="kpi-tile">
            <span class="kpi-label">南線西部平原異常</span>
            <span class="kpi-value">多重潛入波</span>
            <span class="kpi-helper">淺層速度梯度陡峭，近場地動顯著強於傳統岩盤預期</span>
          </div>
        </div>

        <p class="prose">
          傳統認知中，地震學主要聚焦於斷層錯動引起的天然地震；然而梁文宗研究員在這場專題演講中，揭示了「爆炸地震學」如何將地震學轉化為跨足國際安全與公共災害鑑識的「法醫科學」。無論是地下核試爆或都市地下管線氣爆，當現場缺乏直接目擊者或即時感測紀錄時，遍布地表的地震儀波形便是還原事件能量、位置與物理本質的最客觀證詞。
        </p>
        <p class="prose">
          研究團隊利用 <strong>TAIGER 計畫的 10 次人工井穴爆破</strong>觀測資料，在震源時間、空間座標與炸藥量完全已知的條件下，建立了台灣首套針對<strong>近地表爆炸事件的地面最大速度（Peak Ground Velocity, PGV）衰減關係式</strong>，並成功應用於 2014 年高雄氣爆的規模推估（約 <i>M</i><sub>L</sub> 2.38）。同時，南線剖面的異常強震動觀測，更為人口密集的台灣西部平原敲響了防災模型亟需在地化的警鐘。
        </p>
      </section>

      <!-- Section 02: 法醫地震學介紹 -->
      <section id="sec-forensic" class="doc-section">
        <div class="section-head">
          <span class="section-code">02 · Forensic Seismology</span>
          <h2 class="section-title">法醫地震學介紹：<strong>從波形解讀非天然震源的物理真相</strong></h2>
        </div>

        <p class="prose">
          <strong>法醫地震學（Forensic Seismology）</strong>是一門運用地震波觀測資料來偵測、定位並鑑別非天然震源事件（如地下核試爆、礦區爆破、工業意外爆炸、船艦沉沒或大型坍方）的應用科學。其核心精神如同刑事鑑定：震波穿過地殼傳遞至測站後，震源的物理機制會在振幅、頻譜與初動方向上留下無法偽造的「指紋」。
        </p>

        <div class="table-wrap">
          <table>
            <thead>
              <tr>
                <th>比較維度</th>
                <th>天然構造地震（Natural Earthquake）</th>
                <th>地下／近地表爆炸（Explosion Source）</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><strong>物理破裂機制</strong></td>
                <td>斷層面發生<strong>剪切錯動（Double-Couple）</strong>，釋放累積之構造應變能。</td>
                <td>能量瞬間釋放產生<strong>球形向外膨脹（Isotropic Expansion）</strong>，壓縮周圍岩體。</td>
              </tr>
              <tr>
                <td><strong>波相能量分布</strong></td>
                <td>剪切波（S 波）與低頻表面波（Rayleigh / Love 波）發達、持續時間較長。</td>
                <td>能量高度集中於<strong>高頻體波（P 波 / <i>P</i><sub>g</sub> 波）</strong>，表面波相對微弱。</td>
              </tr>
              <tr>
                <td><strong>初動極性特徵</strong></td>
                <td>依測站所在象限呈現「壓縮（＋）」與「膨脹（－）」交替分布。</td>
                <td>各方位角測站初動理論上均為<strong>一致向上的壓縮波（＋）</strong>。</td>
              </tr>
              <tr>
                <td><strong>震源參數掌握</strong></td>
                <td>發震時刻、深度與斷層面積需靠反演推估，參數間存在不確定性與權衡。</td>
                <td>人工爆破實驗可預先精確掌握<strong>時間、位置與炸藥當量</strong>，適合建立經驗公式。</td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="callout">
          <p class="callout-title">為什麼「震源深度」與「震源機制」決定了防災與監測難度？</p>
          <p>
            近地表爆炸發生於極淺層鬆軟沉積物或風化岩層中，其波能激發與近場衰減行為與發生在深部基盤的天然地震截然不同；若缺乏針對性的觀測資料，極易誤判爆炸規模或低估近場震動危害。
          </p>
        </div>
      </section>

      <!-- Section 03: 核試爆波形特徵 -->
      <section id="sec-nuclear" class="doc-section">
        <div class="section-head">
          <span class="section-code">03 · Nuclear Explosion Signatures</span>
          <h2 class="section-title">核試爆波形特徵：<strong>三大物理鑑別指標互動解析</strong></h2>
        </div>

        <p class="prose">
          在國際禁止核試爆監測體系中，科學家必須迅速分辨遠距紀錄究竟來自天然地震還是秘密地下核試爆。演講中特別指出三項核心鑑別依據：<strong>體波規模與表面波規模比（<i>m</i><sub>b</sub> vs. <i>M</i><sub>s</sub>）</strong>、<strong>高頻地殼導波頻譜比（<i>P</i><sub>g</sub> / <i>L</i><sub>g</sub>）</strong>，以及震源機制反演中的<strong>球形膨脹分量</strong>。以下互動模組依演講物理機制呈現三者的辨識邏輯。
        </p>

        <div class="figure-box">
          <div class="tab-bar" role="tablist" aria-label="核試爆鑑別指標切換">
            <button type="button" class="tab-btn is-active" role="tab" aria-selected="true" id="tab-btn-wave" onclick="switchNuclearTab('wave')">
              1. 波形與 <i>P</i><sub>g</sub> / <i>L</i><sub>g</sub> 高頻特徵
            </button>
            <button type="button" class="tab-btn" role="tab" aria-selected="false" id="tab-btn-focal" onclick="switchNuclearTab('focal')">
              2. 震源機制與球形膨脹分量
            </button>
            <button type="button" class="tab-btn" role="tab" aria-selected="false" id="tab-btn-mbms" onclick="switchNuclearTab('mbms')">
              3. <i>m</i><sub>b</sub> 與 <i>M</i><sub>s</sub> 規模鑑別關係
            </button>
          </div>

          <!-- Tab 1: Waveform & Pg/Lg -->
          <div id="panel-wave" class="tab-panel is-active" role="tabpanel" aria-labelledby="tab-btn-wave">
            <div class="control-row">
              <div class="control-group">
                <span class="control-label">濾波頻帶切換 / FILTER BAND</span>
                <div class="btn-group">
                  <button type="button" class="btn is-selected" id="btn-band-broad" onclick="setWaveBand('broad')">寬頻原始波形（Broadband）</button>
                  <button type="button" class="btn" id="btn-band-high" onclick="setWaveBand('high')">高頻濾波（凸顯 <i>P</i><sub>g</sub> / <i>L</i><sub>g</sub> 比值）</button>
                </div>
              </div>
            </div>

            <div class="legend-row">
              <span class="legend-item"><span class="swatch swatch-blue"></span>地下核試爆（瞬間膨脹・高頻體波強）</span>
              <span class="legend-item"><span class="swatch swatch-purple"></span>天然構造地震（剪切錯動・表面波強）</span>
            </div>

            <div class="svg-stage">
              <svg id="svg-waveform" viewBox="0 0 760 280" aria-label="地下核試爆與天然地震波形特徵比較圖">
                <!-- Background grid -->
                <line class="svg-grid" x1="60" y1="75" x2="730" y2="75"></line>
                <line class="svg-grid" x1="60" y1="200" x2="730" y2="200"></line>
                <line class="svg-grid" x1="150" y1="25" x2="150" y2="255"></line>
                <line class="svg-grid" x1="330" y1="25" x2="330" y2="255"></line>
                <line class="svg-grid" x1="500" y1="25" x2="500" y2="255"></line>

                <!-- Phase arrival markers -->
                <text class="svg-text-strong" x="150" y="20" text-anchor="middle">Pg 波抵達</text>
                <text class="svg-text-strong" x="330" y="20" text-anchor="middle">Lg 剪切導波</text>
                <text class="svg-text-strong" x="500" y="20" text-anchor="middle">表面波波列</text>

                <!-- Trace labels -->
                <text class="svg-text-strong" x="12" y="79">核試爆</text>
                <text class="svg-text-strong" x="12" y="204">天然地震</text>

                <!-- Dynamic wave paths populated by JS -->
                <path id="path-wave-exp" class="svg-wave-primary" d=""></path>
                <path id="path-wave-eq" class="svg-wave-compare" d=""></path>

                <!-- X axis -->
                <line class="svg-axis" x1="60" y1="255" x2="730" y2="255"></line>
                <text class="svg-text" x="730" y="272" text-anchor="end">時間演化 Time →</text>
              </svg>
            </div>
            <p class="figure-caption" id="wave-caption">
              寬頻對照：地下爆炸的初至體波（Pg）尖銳且振幅大，但後續表面波甚微；天然地震則擁有漫長且振幅顯著的低頻表面波。切換至「高頻濾波」可觀察核試爆的高 Pg/Lg 比值優勢。
            </p>
          </div>

          <!-- Tab 2: Focal Mechanism & Isotropic Component -->
          <div id="panel-focal" class="tab-panel" role="tabpanel" aria-labelledby="tab-btn-focal">
            <div class="control-row">
              <div class="control-group" style="flex: 1; max-width: 420px;">
                <label class="control-label" for="slider-azimuth">觀測測站方位角 / STATION AZIMUTH：<span id="azimuth-label-val">45°</span></label>
                <input type="range" id="slider-azimuth" min="0" max="360" step="5" value="45" oninput="updateAzimuth(this.value)">
              </div>
            </div>

            <div class="focal-split">
              <div class="focal-card">
                <p class="figure-title">地下核試爆：球形膨脹（Isotropic）</p>
                <p class="figure-units">全象限均呈向外擠壓，無剪力節面</p>
                <svg id="svg-focal-exp" viewBox="0 0 260 220" aria-label="球形膨脹震源機制圖">
                  <circle cx="130" cy="110" r="68" fill="var(--primary-tint)" stroke="var(--data-1)" stroke-width="2"></circle>
                  <!-- Outward radial arrows -->
                  <line x1="130" y1="42" x2="130" y2="22" stroke="var(--data-1)" stroke-width="2"></line>
                  <line x1="130" y1="178" x2="130" y2="198" stroke="var(--data-1)" stroke-width="2"></line>
                  <line x1="62" y1="110" x2="42" y2="110" stroke="var(--data-1)" stroke-width="2"></line>
                  <line x1="198" y1="110" x2="218" y2="110" stroke="var(--data-1)" stroke-width="2"></line>
                  <text class="svg-text-strong" x="130" y="114" text-anchor="middle">+ 全方位壓縮</text>
                  <!-- Station marker -->
                  <circle id="probe-exp" cx="190" cy="50" r="7" fill="var(--on-surface)" stroke="var(--background)" stroke-width="2"></circle>
                </svg>
                <div class="focal-readout">
                  <span>測站初動極性</span>
                  <strong id="polarity-exp" style="color: var(--tertiary);">＋ 壓縮向上（恆正）</strong>
                </div>
              </div>

              <div class="focal-card">
                <p class="figure-title">天然地震：雙力偶剪切（Double-Couple）</p>
                <p class="figure-units">四象限壓縮（＋）／膨脹（－）交替分布</p>
                <svg id="svg-focal-eq" viewBox="0 0 260 220" aria-label="斷層雙力偶震源機制圖">
                  <circle cx="130" cy="110" r="68" fill="var(--background)" stroke="var(--data-2)" stroke-width="2"></circle>
                  <!-- Two shaded compression quadrants (NE & SW) -->
                  <path d="M 130 110 L 130 42 A 68 68 0 0 1 198 110 Z" fill="var(--data-2-tint)"></path>
                  <path d="M 130 110 L 130 178 A 68 68 0 0 1 62 110 Z" fill="var(--data-2-tint)"></path>
                  <!-- Nodal planes -->
                  <line x1="130" y1="42" x2="130" y2="178" stroke="var(--data-2)" stroke-width="1.5" stroke-dasharray="4 3"></line>
                  <line x1="62" y1="110" x2="198" y2="110" stroke="var(--data-2)" stroke-width="1.5" stroke-dasharray="4 3"></line>
                  <text class="svg-text-strong" x="164" y="82" text-anchor="middle">+</text>
                  <text class="svg-text-strong" x="96" y="144" text-anchor="middle">+</text>
                  <text class="svg-text" x="96" y="82" text-anchor="middle">−</text>
                  <text class="svg-text" x="164" y="144" text-anchor="middle">−</text>
                  <!-- Station marker -->
                  <circle id="probe-eq" cx="190" cy="50" r="7" fill="var(--on-surface)" stroke="var(--background)" stroke-width="2"></circle>
                </svg>
                <div class="focal-readout">
                  <span>測站初動極性</span>
                  <strong id="polarity-eq" style="color: var(--data-2);">＋ 壓縮（東北象限）</strong>
                </div>
              </div>
            </div>
            <p class="figure-caption">
              操作提示：拖曳方位角滑桿旋轉虛擬測站。核試爆於任何方位角皆呈現一致向上的壓縮初動（球形膨脹分量佔主導）；天然地震則隨斷層象限切換正負極性。
            </p>
          </div>

          <!-- Tab 3: mb vs Ms -->
          <div id="panel-mbms" class="tab-panel" role="tabpanel" aria-labelledby="tab-btn-mbms">
            <div class="legend-row">
              <span class="legend-item"><span class="swatch swatch-purple"></span>天然地震趨勢群（表面波 <i>M</i><sub>s</sub> 較高）</span>
              <span class="legend-item"><span class="swatch swatch-blue"></span>地下核試爆趨勢群（體波 <i>m</i><sub>b</sub> 主導，<i>M</i><sub>s</sub> 偏低）</span>
            </div>
            <div class="svg-stage">
              <svg viewBox="0 0 760 280" aria-label="體波規模 mb 與表面波規模 Ms 鑑別概念圖">
                <!-- Grid -->
                <line class="svg-grid" x1="80" y1="50" x2="710" y2="50"></line>
                <line class="svg-grid" x1="80" y1="110" x2="710" y2="110"></line>
                <line class="svg-grid" x1="80" y1="170" x2="710" y2="170"></line>
                <line class="svg-grid" x1="80" y1="230" x2="710" y2="230"></line>
                <line class="svg-axis" x1="80" y1="30" x2="80" y2="230"></line>
                <line class="svg-axis" x1="80" y1="230" x2="710" y2="230"></line>

                <!-- Earthquake envelope band -->
                <polygon points="130,205 640,35 675,65 165,222" fill="var(--data-2-tint)"></polygon>
                <!-- Explosion envelope band -->
                <polygon points="180,224 660,115 680,148 210,228" fill="var(--primary-tint)"></polygon>

                <!-- Discriminant threshold line -->
                <line x1="120" y1="224" x2="690" y2="75" stroke="var(--on-surface)" stroke-width="2" stroke-dasharray="6 4"></line>
                <text class="svg-text-strong" x="520" y="102" transform="rotate(-14.5 520 102)">經驗鑑別分界線</text>

                <!-- Representative schematic points -->
                <circle cx="210" cy="182" r="5" fill="var(--data-2)"></circle>
                <circle cx="265" cy="160" r="5" fill="var(--data-2)"></circle>
                <circle cx="320" cy="145" r="5" fill="var(--data-2)"></circle>
                <circle cx="385" cy="120" r="5" fill="var(--data-2)"></circle>
                <circle cx="445" cy="105" r="5" fill="var(--data-2)"></circle>
                <circle cx="520" cy="80" r="5" fill="var(--data-2)"></circle>
                <circle cx="590" cy="60" r="5" fill="var(--data-2)"></circle>

                <rect x="275" y="198" width="9" height="9" fill="var(--data-1)"></rect>
                <rect x="335" y="182" width="9" height="9" fill="var(--data-1)"></rect>
                <rect x="405" y="168" width="9" height="9" fill="var(--data-1)"></rect>
                <rect x="475" y="152" width="9" height="9" fill="var(--data-1)"></rect>
                <rect x="545" y="138" width="9" height="9" fill="var(--data-1)"></rect>
                <rect x="610" y="124" width="9" height="9" fill="var(--data-1)"></rect>

                <!-- Direct labels -->
                <text class="svg-text-strong" x="180" y="128" fill="var(--data-2)">天然地震群（同 mb 下 Ms 較大）</text>
                <text class="svg-text-strong" x="455" y="200" fill="var(--data-1)">地下核試爆群（體波集中、Ms 顯著偏低）</text>

                <text class="svg-text-strong" x="395" y="262" text-anchor="middle">體波規模 mb（Body-Wave Magnitude）→</text>
                <text class="svg-text-strong" x="26" y="135" text-anchor="middle" transform="rotate(-90 26 135)">表面波規模 Ms →</text>
              </svg>
            </div>
            <p class="figure-caption">
              概念示意圖：當體波規模 <i>m</i><sub>b</sub> 相近時，地下爆炸因缺乏持續的斷層剪切破裂，所激發的表面波規模 <i>M</i><sub>s</sub> 遠低於天然地震，因此在 <i>m</i><sub>b</sub>–<i>M</i><sub>s</sub> 平面上明顯落於分界線下方。
            </p>
          </div>
        </div>
      </section>

      <!-- Section 04: TAIGER 炸測實驗 -->
      <section id="sec-taiger" class="doc-section">
        <div class="section-head">
          <span class="section-code">04 · TAIGER Controlled Explosions</span>
          <h2 class="section-title">TAIGER 炸測實驗：<strong>10 次人工井穴爆破如何克服震源黑箱</strong></h2>
        </div>

        <p class="prose">
          過去建立地震動衰減關係式多依賴天然地震紀錄，然而天然地震的發震時刻、斷層幾何與能量釋放過程均為未知數，必須透過反演估算，導致模型存在高度不確定性。為突破這項限制，研究團隊運用 <strong>TAIGER 計畫所執行的 10 次人工井穴爆破（Borehole Explosions）</strong>作為研究基礎。
        </p>

        <ol class="pipeline-list">
          <li class="pipeline-item">
            <span class="pipeline-step">Step 01</span>
            <div class="pipeline-body">
              <h3>精確已知的三項核心震源參數</h3>
              <p>每一次人工井穴爆破的<strong>起爆時間（Origin Time）</strong>、<strong>精確經緯度與井深（Location &amp; Depth）</strong>，以及<strong>裝填炸藥量（Charge Weight）</strong>均由實驗設計完全掌握，徹底消除了天然地震震源定位與規模估算的誤差源。</p>
            </div>
          </li>
          <li class="pipeline-item">
            <span class="pipeline-step">Step 02</span>
            <div class="pipeline-body">
              <h3>純化地殼路徑與場址衰減效應</h3>
              <p>當震源端成為已知常數，測站所記錄到的地面最大速度（PGV）隨距離衰減的變化，便能更純粹地反映地殼介質的非彈性衰減（Anelastic Attenuation）、幾何擴散與淺層地質構造效應。</p>
            </div>
          </li>
          <li class="pipeline-item">
            <span class="pipeline-step">Step 03</span>
            <div class="pipeline-body">
              <h3>建立首套近地表爆炸 PGV 衰減關係式</h3>
              <p>研究團隊彙整 10 次爆破於不同距離測站所測得之 PGV 數據進行迴歸擬合，成功建構了針對近地表爆炸事件的 PGV 衰減經驗式，填補過去缺乏極淺層非天然震源評估模型的空白。</p>
            </div>
          </li>
        </ol>
      </section>

      <!-- Section 05: PGV 衰減關係式擬合與南線異常 -->
      <section id="sec-attenuation" class="doc-section">
        <div class="section-head">
          <span class="section-code">05 · PGV Attenuation &amp; Southern Line Anomaly</span>
          <h2 class="section-title">PGV 衰減關係式擬合：<strong>南線多重潛入波與西部平原放大警訊</strong></h2>
        </div>

        <p class="prose">
          在檢視 TAIGER 各測線的觀測結果時，研究團隊在<strong>南線（Southern Line）</strong>發現了出乎意料的現象：與山區堅硬岩盤區的衰減預期相比，西部平原與麓山帶的近場地動速度明顯偏強。物理追因顯示，西部平原與麓山帶極為陡峭的淺層速度梯度，使向下傳播的震波迅速折返地表，形成<strong>多重潛入波（Multiple Diving Waves）</strong>於近場疊加增強。
        </p>

        <!-- Interactive Figure A: Ray-Path Velocity Gradient -->
        <div class="figure-box">
          <div class="figure-header">
            <h3 class="figure-title">互動剖面：淺層速度梯度如何產生「多重潛入波」</h3>
            <span class="figure-units">Ray-Path Schematic · 概念機制對照</span>
          </div>

          <div class="control-row">
            <div class="control-group">
              <span class="control-label">地質剖面模式切換 / GEOLOGIC SETTING</span>
              <div class="btn-group">
                <button type="button" class="btn is-selected" id="btn-ray-rock" onclick="setRayMode('rock')">山區岩盤基準（緩慢速度梯度）</button>
                <button type="button" class="btn" id="btn-ray-plain" onclick="setRayMode('plain')">南線：西部平原／麓山帶（陡峭梯度）</button>
              </div>
            </div>
          </div>

          <div class="svg-stage">
            <svg id="svg-raypath" viewBox="0 0 760 270" aria-label="山區岩盤與西部平原多重潛入波波線比較圖">
              <!-- Surface and Depth Layers -->
              <rect id="layer-shallow" x="140" y="36" width="600" height="64" fill="var(--surface-container)"></rect>
              <rect id="layer-deep" x="140" y="100" width="600" height="140" fill="var(--background)"></rect>
              <line x1="140" y1="36" x2="740" y2="36" stroke="var(--on-surface)" stroke-width="2"></line>
              <line x1="140" y1="100" x2="740" y2="100" stroke="var(--outline-variant)" stroke-width="1" stroke-dasharray="4 3"></line>

              <!-- Left Velocity Profile Box -->
              <line class="svg-axis" x1="30" y1="36" x2="115" y2="36"></line>
              <line class="svg-axis" x1="30" y1="36" x2="30" y2="235"></line>
              <text class="svg-text" x="72" y="25" text-anchor="middle">速度 V(z) →</text>
              <text class="svg-text" x="18" y="140" text-anchor="middle" transform="rotate(-90 18 140)">深度 Depth ↓</text>
              <path id="vel-profile-path" d="M 45 36 L 62 100 L 95 230" stroke="var(--data-3)" stroke-width="2.5" fill="none"></path>

              <!-- Source star/circle at near-surface -->
              <circle cx="170" cy="44" r="6" fill="var(--error)"></circle>
              <text class="svg-text-strong" x="170" y="24" text-anchor="middle">近地表爆源</text>

              <!-- Receiver markers -->
              <polygon points="340,36 334,26 346,26" fill="var(--on-surface)"></polygon>
              <polygon points="480,36 474,26 486,26" fill="var(--on-surface)"></polygon>
              <polygon points="620,36 614,26 626,26" fill="var(--on-surface)"></polygon>
              <text class="svg-text" x="480" y="20" text-anchor="middle">近場測站群（PGV 觀測）</text>

              <!-- Dynamic Ray Paths -->
              <g id="ray-group-rock">
                <path d="M 170 44 Q 260 110 340 36" class="svg-wave-context"></path>
                <path d="M 170 44 Q 340 165 480 36" class="svg-wave-context"></path>
                <path d="M 170 44 Q 420 215 620 36" class="svg-wave-context"></path>
                <text class="svg-text-strong" x="440" y="192">波線深入基盤後折返・能量隨幾何擴散穩定衰減</text>
              </g>

              <g id="ray-group-plain" style="display: none;">
                <!-- Steep bending shallow diving waves -->
                <path d="M 170 44 Q 255 96 340 36" class="svg-wave-primary"></path>
                <path d="M 170 44 Q 255 96 340 36 Q 410 92 480 36" class="svg-wave-primary"></path>
                <path d="M 170 44 Q 255 96 340 36 Q 410 92 480 36 Q 550 92 620 36" class="svg-wave-primary"></path>
                <path d="M 170 44 Q 325 128 480 36" class="svg-wave-compare"></path>
                <circle cx="480" cy="40" r="14" fill="var(--primary-tint)" stroke="var(--data-1)" stroke-width="1.5"></circle>
                <text class="svg-text-strong" x="440" y="148" fill="var(--data-1)">淺層陡峭速度梯度使波線急劇上彎，形成「多重潛入波」於近場疊加放大</text>
              </g>
            </svg>
          </div>
          <p class="figure-caption" id="ray-caption">
            目前顯示：山區岩盤基準剖面。岩盤隨深度速度變化較為平緩，震波向下穿透較深後再折返，近場 PGV 符合一般岩盤衰減預期。切換至「南線：西部平原／麓山帶」觀察淺層速度梯度的聚焦效應。
          </p>
        </div>

        <!-- Interactive Figure B: Conceptual PGV Attenuation Curve -->
        <div class="figure-box">
          <div class="figure-header">
            <h3 class="figure-title">互動趨勢模擬：PGV 距離衰減與平原近場低估風險</h3>
            <span class="figure-units">相對正規化 PGV 指標（對數座標概念趨勢）</span>
          </div>

          <div class="control-row">
            <div class="control-group">
              <span class="control-label">事件規模預設 / EVENT PRESET</span>
              <div class="btn-group">
                <button type="button" class="btn" id="btn-preset-small" onclick="setAttenPreset(1.50)">小型爆破 <i>M</i><sub>L</sub> 1.50</button>
                <button type="button" class="btn is-selected" id="btn-preset-kh" onclick="setAttenPreset(2.38)">高雄氣爆 <i>M</i><sub>L</sub> 2.38</button>
                <button type="button" class="btn" id="btn-preset-large" onclick="setAttenPreset(3.00)">較大事件 <i>M</i><sub>L</sub> 3.00</button>
              </div>
            </div>
            <div class="control-group">
              <span class="control-label">場址條件 / SITE MODEL</span>
              <button type="button" class="btn is-selected" id="btn-toggle-plain-curve" onclick="togglePlainCurve()">已開啟：南線平原多重潛入波效應</button>
            </div>
          </div>

          <div class="control-row">
            <div class="control-group" style="flex: 1; max-width: 460px;">
              <label class="control-label" for="slider-dist">震央距離檢視 / EPICENTRAL DISTANCE R：<span id="dist-label-val">8 km（近場）</span></label>
              <input type="range" id="slider-dist" min="2" max="50" step="1" value="8" oninput="updateDistanceReadout(this.value)">
            </div>
          </div>

          <div class="legend-row">
            <span class="legend-item"><span class="swatch swatch-gray"></span>岩盤預期衰減曲線（Baseline Rock Model）</span>
            <span class="legend-item"><span class="swatch swatch-blue"></span>南線西部平原趨勢（含多重潛入波近場增強）</span>
          </div>

          <div class="svg-stage">
            <svg id="svg-atten" viewBox="0 0 760 270" aria-label="PGV 隨距離衰減概念曲線與近場放大比較圖">
              <line class="svg-grid" x1="80" y1="40" x2="720" y2="40"></line>
              <line class="svg-grid" x1="80" y1="95" x2="720" y2="95"></line>
              <line class="svg-grid" x1="80" y1="150" x2="720" y2="150"></line>
              <line class="svg-grid" x1="80" y1="205" x2="720" y2="205"></line>
              <line class="svg-axis" x1="80" y1="25" x2="80" y2="225"></line>
              <line class="svg-axis" x1="80" y1="225" x2="720" y2="225"></line>

              <text class="svg-text" x="70" y="44" text-anchor="end">10²</text>
              <text class="svg-text" x="70" y="99" text-anchor="end">10¹</text>
              <text class="svg-text" x="70" y="154" text-anchor="end">10⁰</text>
              <text class="svg-text" x="70" y="209" text-anchor="end">10⁻¹</text>

              <text class="svg-text" x="80" y="242" text-anchor="middle">2 km</text>
              <text class="svg-text" x="240" y="242" text-anchor="middle">10 km</text>
              <text class="svg-text" x="480" y="242" text-anchor="middle">25 km</text>
              <text class="svg-text" x="720" y="242" text-anchor="middle">50 km</text>

              <text class="svg-text-strong" x="400" y="262" text-anchor="middle">震央距離 Distance R (km) →</text>
              <text class="svg-text-strong" x="24" y="125" text-anchor="middle" transform="rotate(-90 24 125)">相對 PGV 強度 (log) →</text>

              <!-- Dynamic paths -->
              <path id="path-atten-rock" class="svg-wave-context" stroke-dasharray="5 4" d=""></path>
              <path id="path-atten-plain" class="svg-wave-primary" d=""></path>

              <!-- Crosshair -->
              <line id="atten-crosshair" x1="200" y1="25" x2="200" y2="225" stroke="var(--on-surface)" stroke-width="1" stroke-dasharray="3 3"></line>
              <circle id="dot-atten-rock" cx="200" cy="140" r="5" fill="var(--data-context)"></circle>
              <circle id="dot-atten-plain" cx="200" cy="110" r="6" fill="var(--data-1)"></circle>
            </svg>
          </div>

          <div class="attenuation-readout">
            <div class="readout-cell">
              <span class="kpi-label">當前選定事件規模</span>
              <span class="readout-val is-primary" id="readout-mag"><i>M</i><sub>L</sub> 2.38</span>
            </div>
            <div class="readout-cell">
              <span class="kpi-label">岩盤預期相對 PGV</span>
              <span class="readout-val" id="readout-rock">1.32×</span>
            </div>
            <div class="readout-cell">
              <span class="kpi-label">南線平原預期相對 PGV</span>
              <span class="readout-val is-alert" id="readout-plain">2.36×</span>
            </div>
            <div class="readout-cell">
              <span class="kpi-label">近場效應差異評估</span>
              <span class="readout-val" id="readout-ratio">平原強 +79%</span>
            </div>
          </div>

          <p class="figure-caption">
            模型說明：此互動圖表依據演講結論呈現「距離衰減趨勢」與「南線近場潛入波放大」之物理對比關係（以 <i>M</i><sub>L</sub> 2.38、距離 10 km 之岩盤基準為 1.00× 正規化單位），藉此說明直接套用岩盤公式在近場將低估平原區實際地動強度。
          </p>
        </div>

        <div class="callout callout-warning">
          <p class="callout-title">防災核心警訊：不能直接套用山區岩盤公式</p>
          <p>
            台灣絕大多數的人口、住宅與高科技及石化產業皆集中於西部平原。若在災害評估時直接沿用山區岩盤的震動衰減公式，將系統性低估近場潛入波所帶來的強地動風險。建立西部平原專屬的衰減方程式，是未來極具迫切性的研究方向。
          </p>
        </div>
      </section>

      <!-- Section 06: 高雄氣爆實例應用 -->
      <section id="sec-kaohsiung" class="doc-section">
        <div class="section-head">
          <span class="section-code">06 · 2014 Kaohsiung Gas Explosion Case Study</span>
          <h2 class="section-title">高雄氣爆實例應用：<strong>從基礎研究落實到都市公共安全</strong></h2>
        </div>

        <p class="prose">
          2014 年發生的<strong>高雄氣爆事件</strong>屬於極淺層、沿都市地下箱涵與管線發生之氣體爆炸，其震源性質完全不同於天然斷層錯動。這類重大公共安全事故發生後，如何在第一時間客觀定量評估爆炸能量與規模，一直是災後鑑識與應變的難題。
        </p>

        <div class="card-grid">
          <div class="card-tile">
            <div class="card-tile-head">
              <h3 class="card-tile-title">應用契機與模型嫁接</h3>
              <span class="card-tile-code">METHODOLOGY</span>
            </div>
            <p class="prose-muted" style="margin: 0;">
              過去由於缺乏近地表爆炸專屬衰減式，若套用深部天然地震規模公式往往產生偏差。研究團隊將 TAIGER 10 次人工井穴爆破所建立之<strong>近地表爆炸 PGV 衰減關係式</strong>，直接應用於高雄氣爆周邊地震測站所錄得的實際地面速度紀錄。
            </p>
          </div>
          <div class="card-tile">
            <div class="card-tile-head">
              <h3 class="card-tile-title">推估規模成果：<i>M</i><sub>L</sub> 2.38</h3>
              <span class="card-tile-code">FINDING</span>
            </div>
            <p class="prose-muted" style="margin: 0;">
              透過測站分布與 PGV 隨距離衰減之擬合反推，計算出 2014 年高雄氣爆的等效地震規模約為 <strong><i>M</i><sub>L</sub> 2.38</strong>。這證明了基礎爆炸地震學研究不僅止於學術論文，更能精確量化都市災難的物理能量尺度。
            </p>
          </div>
        </div>

        <div class="callout callout-positive">
          <p class="callout-title">基礎科學的公共安全價值</p>
          <p>
            高雄氣爆的規模推估示範了一個典範轉移：藉由預先建置的精密物理實驗（TAIGER 井穴爆破），讓原本針對地殼成像與基礎研究設計的測站網路，在重大人為事故發生時立刻發揮「法醫級」量化鑑識功能。
          </p>
        </div>
      </section>

      <!-- Section 07: 專題心得與討論 -->
      <section id="sec-reflection" class="doc-section">
        <div class="section-head">
          <span class="section-code">07 · Reflections &amp; Discussion</span>
          <h2 class="section-title">專題心得與討論：<strong>重新認識地震學的科學疆界與社會責任</strong></h2>
        </div>

        <div class="reflection-list">
          <div class="reflection-item">
            <h3>一、從天然災害研究走向「法醫地震學」的震撼</h3>
            <p>
              過去我一直以為地震學只專注於研究板塊運動與天然構造地震，這場演講徹底打破了這個刻板印象，讓我看到地震學也能扮演「法醫」的角色——當重大爆炸事件沒有目擊者時，地震儀所記錄到的波形就是最客觀、無可辯駁的物理證詞。特別是在地下核試爆與天然地震的鑑別上，透過 <i>m</i><sub>b</sub> 與 <i>M</i><sub>s</sub> 的規模對比、<i>P</i><sub>g</sub>/<i>L</i><sub>g</sub> 高頻頻譜比，以及震源機制中的球形膨脹分量，就能從純粹的波形數據拆穿人為試爆與自然錯動的差異。這是我第一次系統性理解這套鑑別機制，也深刻體會到科學數據在國際安全監測中的關鍵分量。
            </p>
          </div>

          <div class="reflection-item">
            <h3>二、人工可控爆破實驗的精準度與公共安全實踐</h3>
            <p>
              第二個令我印象深刻的重點，是 TAIGER 計畫所執行的 10 次人工井穴爆破。相較於天然地震在發震時間、震源位置與釋放能量上的高度不確定性，人工爆破的時間、空間座標與炸藥量皆完全已知，正好補足了天然地震資料的先天缺陷。研究團隊據此建立了台灣第一個近地表爆炸的 PGV 衰減關係式，並進一步將其應用於 2014 年高雄氣爆，推估出相當於 <i>M</i><sub>L</sub> 2.38 的規模。這種把基礎地球物理觀測扎實落實到都市公共安全鑑識的歷程，是最令人佩服的研究示範。
            </p>
          </div>

          <div class="reflection-item">
            <h3>三、南線多重潛入波對西部平原防災的深遠啟示</h3>
            <p>
              最令我感到意外的，是南線剖面的異常觀測結果。西部平原與麓山帶極為陡峭的淺層速度梯度，誘發了多重潛入波，使得近場地動速度遠強於傳統岩盤公式的預期。這項發現提醒我們，災害評估絕對不能直接將山區岩盤的經驗公式套用到其他地質環境，否則只會低估平原區的真實受災風險。考量到台灣絕大多數的人口與核心產業都高度集中於西部平原，未來投入資源建立「西部平原專屬」的震動衰減方程式，將是極為迫切且重要的防災工程。
            </p>
          </div>

          <div class="reflection-item">
            <h3>四、總結反思：嚴謹的觀測與模型是理解災害的起點</h3>
            <p>
              整場演講不僅拓展了我對地震學應用範疇的視野，更讓我深切理解到：無論面對的是地下核試爆監測、都市氣爆規模回溯，或是平原區強地動預測，唯有建立在嚴謹野外觀測與物理模型上的科學推論，才能真正成為守護社會安全的堅實基礎。
            </p>
          </div>
        </div>

        <!-- Interactive Concept Check -->
        <div class="quiz-card" aria-label="演講核心概念檢核">
          <p class="section-code" style="margin-bottom: var(--space-xs);">Concept Check · 核心重點快速檢核</p>
          <p class="quiz-q" id="quiz-question-text">
            問題 1 / 3：為何在相同體波規模 <i>m</i><sub>b</sub> 下，地下核試爆的表面波規模 <i>M</i><sub>s</sub> 通常顯著低於天然地震？
          </p>
          <div class="quiz-options" id="quiz-options-container">
            <button type="button" class="quiz-opt" onclick="answerQuiz(0)">A. 地下爆炸由斷層剪切錯動主導，使體波完全消失</button>
            <button type="button" class="quiz-opt" onclick="answerQuiz(1)">B. 地下爆炸為瞬間向外球形膨脹，能量高度集中於高頻體波，較少激發低頻表面波</button>
            <button type="button" class="quiz-opt" onclick="answerQuiz(2)">C. 地下爆炸必定發生在超過 100 公里的深部地函中</button>
          </div>
          <div class="quiz-feedback" id="quiz-feedback"></div>
          <div class="control-row" style="margin-top: var(--space-md); margin-bottom: 0;">
            <button type="button" class="btn" id="btn-quiz-next" onclick="nextQuizQuestion()">下一題（2 / 3）</button>
          </div>
        </div>
      </section>

    </main>
  </div>

  <!-- Document Footer -->
  <footer class="doc-footer">
    <div class="doc-footer-inner">
      <div>
        <strong>爆炸地震學演講紀錄與心得整理</strong> · 主講人：梁文宗 研究員
      </div>
      <div>
        內容依據演講核心紀錄與專題心得彙整建置；互動圖表用於物理機制與衰減趨勢視覺化說明。
      </div>
    </div>
  </footer>

  <script>
    // 1. Scroll-spy for sidebar & mobile TOC
    function initScrollSpy() {
      const sections = document.querySelectorAll('.doc-section');
      const sideLinks = document.querySelectorAll('.side-nav-list a');
      const mobileLinks = document.querySelectorAll('.mobile-toc a');

      if (!sections.length) return;

      const observer = new IntersectionObserver(
        function (entries) {
          entries.forEach(function (entry) {
            if (!entry.isIntersecting) return;
            const id = entry.target.getAttribute('id');
            if (!id) return;

            sideLinks.forEach(function (link) {
              const href = link.getAttribute('href');
              if (href === `#${id}`) {
                link.classList.add('is-active');
              } else {
                link.classList.remove('is-active');
              }
            });

            mobileLinks.forEach(function (link) {
              const href = link.getAttribute('href');
              if (href === `#${id}`) {
                link.classList.add('is-active');
              } else {
                link.classList.remove('is-active');
              }
            });
          });
        },
        { rootMargin: '-15% 0px -70% 0px', threshold: 0.05 }
      );

      sections.forEach(function (sec) {
        observer.observe(sec);
      });
    }

    // 2. Section 03: Nuclear Explosion Tabs & Waveform / Focal Explorers
    let currentWaveBand = 'broad';

    function switchNuclearTab(tabName) {
      const tabs = ['wave', 'focal', 'mbms'];
      tabs.forEach(function (name) {
        const btn = document.getElementById(`tab-btn-${name}`);
        const panel = document.getElementById(`panel-${name}`);
        if (btn) {
          if (name === tabName) {
            btn.classList.add('is-active');
            btn.setAttribute('aria-selected', 'true');
          } else {
            btn.classList.remove('is-active');
            btn.setAttribute('aria-selected', 'false');
          }
        }
        if (panel) {
          if (name === tabName) {
            panel.classList.add('is-active');
          } else {
            panel.classList.remove('is-active');
          }
        }
      });
    }

    function buildWavePath(baseY, type, band) {
      const startX = 60;
      const endX = 720;
      const step = 3;
      const points = [];

      for (let x = startX; x <= endX; x += step) {
        let amp = 0;

        if (type === 'exp') {
          // Explosion: sharp high-freq Pg around x=150..230, weak Lg around x=330, tiny surface wave
          const pgEnv = x >= 145 ? Math.exp(-Math.pow((x - 175) / 28, 2)) : 0;
          const lgEnv = x >= 315 ? Math.exp(-Math.pow((x - 350) / 36, 2)) : 0;
          const surfEnv = x >= 470 ? Math.exp(-Math.pow((x - 530) / 55, 2)) : 0;

          if (band === 'broad') {
            amp = pgEnv * 44 * Math.sin((x - 145) * 0.65)
                + lgEnv * 14 * Math.sin((x - 315) * 0.42)
                + surfEnv * 6 * Math.sin((x - 470) * 0.14);
          } else {
            // High-frequency filter highlights Pg/Lg ratio starkly
            amp = pgEnv * 50 * Math.sin((x - 145) * 0.95)
                + lgEnv * 11 * Math.sin((x - 315) * 0.85);
          }
        } else {
          // Natural earthquake: moderate Pg, strong Lg, large low-freq surface waves
          const pgEnv = x >= 145 ? Math.exp(-Math.pow((x - 185) / 32, 2)) : 0;
          const lgEnv = x >= 310 ? Math.exp(-Math.pow((x - 375) / 48, 2)) : 0;
          const surfEnv = x >= 445 ? Math.exp(-Math.pow((x - 545) / 72, 2)) : 0;

          if (band === 'broad') {
            amp = pgEnv * 16 * Math.sin((x - 145) * 0.55)
                + lgEnv * 32 * Math.sin((x - 310) * 0.36)
                + surfEnv * 44 * Math.sin((x - 445) * 0.14);
          } else {
            // High-freq filter attenuates low-freq surface waves, leaving moderate Pg and stronger Lg
            amp = pgEnv * 17 * Math.sin((x - 145) * 0.9)
                + lgEnv * 30 * Math.sin((x - 310) * 0.82)
                + surfEnv * 5 * Math.sin((x - 445) * 0.7);
          }
        }

        const y = (baseY - amp).toFixed(1);
        points.push(`${x === startX ? 'M' : 'L'} ${x} ${y}`);
      }
      return points.join(' ');
    }

    function renderWaveforms() {
      const expEl = document.getElementById('path-wave-exp');
      const eqEl = document.getElementById('path-wave-eq');
      if (expEl) expEl.setAttribute('d', buildWavePath(75, 'exp', currentWaveBand));
      if (eqEl) eqEl.setAttribute('d', buildWavePath(200, 'eq', currentWaveBand));
    }

    function setWaveBand(band) {
      currentWaveBand = band;
      const btnBroad = document.getElementById('btn-band-broad');
      const btnHigh = document.getElementById('btn-band-high');
      const caption = document.getElementById('wave-caption');

      if (btnBroad && btnHigh) {
        if (band === 'broad') {
          btnBroad.classList.add('is-selected');
          btnHigh.classList.remove('is-selected');
        } else {
          btnBroad.classList.remove('is-selected');
          btnHigh.classList.add('is-selected');
        }
      }

      if (caption) {
        caption.textContent = band === 'broad'
          ? `寬頻對照：地下爆炸的初至體波（Pg）尖銳且振幅大，但後續表面波甚微；天然地震則擁有漫長且振幅顯著的低頻表面波。切換至「高頻濾波」可觀察核試爆的高 Pg/Lg 比值優勢。`
          : `高頻濾波對照：濾除低頻表面波後，核試爆展現極高的 Pg / Lg 振幅比（體波能量集中）；天然地震則維持較顯著的 Lg 剪切導波，使兩者在頻譜特徵上清晰分離。`;
      }

      renderWaveforms();
    }

    function updateAzimuth(val) {
      const deg = Number(val);
      const label = document.getElementById('azimuth-label-val');
      if (label) label.textContent = `${deg}°`;

      // Convert compass azimuth (0 deg = North/top, clockwise)
      const rad = (deg - 90) * (Math.PI / 180);
      const cx = 130 + 68 * Math.cos(rad);
      const cy = 110 + 68 * Math.sin(rad);

      const probeExp = document.getElementById('probe-exp');
      const probeEq = document.getElementById('probe-eq');
      if (probeExp) {
        probeExp.setAttribute('cx', cx.toFixed(1));
        probeExp.setAttribute('cy', cy.toFixed(1));
      }
      if (probeEq) {
        probeEq.setAttribute('cx', cx.toFixed(1));
        probeEq.setAttribute('cy', cy.toFixed(1));
      }

      const polEq = document.getElementById('polarity-eq');
      if (polEq) {
        const isNodal = (deg % 90 === 0);
        if (isNodal) {
          polEq.textContent = `0 節面位置（振幅近零）`;
          polEq.style.color = 'var(--on-surface-variant)';
        } else if ((deg > 0 && deg < 90) || (deg > 180 && deg < 270)) {
          const quad = deg < 90 ? `東北象限` : `西南象限`;
          polEq.textContent = `＋ 壓縮（${quad}）`;
          polEq.style.color = 'var(--data-2)';
        } else {
          const quad = deg > 270 ? `西北象限` : `東南象限`;
          polEq.textContent = `－ 膨脹（${quad}）`;
          polEq.style.color = 'var(--error)';
        }
      }
    }

    // 3. Section 05: Ray-path toggle & PGV Attenuation Explorer
    let attenMag = 2.38;
    let showPlainEffect = true;
    let attenDist = 8;

    function setRayMode(mode) {
      const rockGroup = document.getElementById('ray-group-rock');
      const plainGroup = document.getElementById('ray-group-plain');
      const velPath = document.getElementById('vel-profile-path');
      const btnRock = document.getElementById('btn-ray-rock');
      const btnPlain = document.getElementById('btn-ray-plain');
      const caption = document.getElementById('ray-caption');

      if (mode === 'rock') {
        if (rockGroup) rockGroup.style.display = 'inline';
        if (plainGroup) plainGroup.style.display = 'none';
        if (velPath) velPath.setAttribute('d', 'M 45 36 L 62 100 L 95 230');
        if (btnRock) btnRock.classList.add('is-selected');
        if (btnPlain) btnPlain.classList.remove('is-selected');
        if (caption) {
          caption.textContent = `目前顯示：山區岩盤基準剖面。岩盤隨深度速度變化較為平緩，震波向下穿透較深後再折返，近場 PGV 符合一般岩盤衰減預期。切換至「南線：西部平原／麓山帶」觀察淺層速度梯度的聚焦效應。`;
        }
      } else {
        if (rockGroup) rockGroup.style.display = 'none';
        if (plainGroup) plainGroup.style.display = 'inline';
        if (velPath) velPath.setAttribute('d', 'M 36 36 Q 82 65 98 100 L 108 230');
        if (btnRock) btnRock.classList.remove('is-selected');
        if (btnPlain) btnPlain.classList.add('is-selected');
        if (caption) {
          caption.textContent = `目前顯示：南線（西部平原與麓山帶）。極為陡峭的淺層速度梯度使震波在淺層急劇折返，產生「多重潛入波（Multiple Diving Waves）」並於近場測站疊加，導致實際地動比岩盤預期更強。`;
        }
      }
    }

    // Normalized conceptual attenuation model anchored at ML 2.38, R = 10 km -> Rock = 1.00
    function calcRelativePgv(mag, distKm, isPlain) {
      const magFactor = Math.pow(10, 0.72 * (mag - 2.38));
      const rockVal = magFactor * Math.pow(10 / distKm, 1.35);
      if (!isPlain) return rockVal;
      // Near-field shallow diving wave boost peaking around 4-15 km and tapering at larger distance
      const boost = 1 + 0.92 * Math.exp(-Math.pow((distKm - 7) / 11, 2));
      return rockVal * boost;
    }

    function distToSvgX(distKm) {
      return 80 + ((distKm - 2) / 48) * 640;
    }

    function pgvToSvgY(val) {
      const logV = Math.log10(Math.max(val, 0.03));
      // logV = 2 -> y=40, logV = -1 -> y=205
      const y = 150 - logV * 55;
      return Math.max(25, Math.min(222, y));
    }

    function renderAttenuationChart() {
      const rockPts = [];
      const plainPts = [];

      for (let r = 2; r <= 50; r += 1) {
        const x = distToSvgX(r).toFixed(1);
        const yRock = pgvToSvgY(calcRelativePgv(attenMag, r, false)).toFixed(1);
        const yPlain = pgvToSvgY(calcRelativePgv(attenMag, r, true)).toFixed(1);
        rockPts.push(`${r === 2 ? 'M' : 'L'} ${x} ${yRock}`);
        plainPts.push(`${r === 2 ? 'M' : 'L'} ${x} ${yPlain}`);
      }

      const rockPath = document.getElementById('path-atten-rock');
      const plainPath = document.getElementById('path-atten-plain');
      const cross = document.getElementById('atten-crosshair');
      const dotRock = document.getElementById('dot-atten-rock');
      const dotPlain = document.getElementById('dot-atten-plain');

      if (rockPath) rockPath.setAttribute('d', rockPts.join(' '));
      if (plainPath) {
        plainPath.setAttribute('d', plainPts.join(' '));
        plainPath.style.display = showPlainEffect ? 'inline' : 'none';
      }

      const cx = distToSvgX(attenDist).toFixed(1);
      const vRock = calcRelativePgv(attenMag, attenDist, false);
      const vPlain = calcRelativePgv(attenMag, attenDist, true);
      const cyRock = pgvToSvgY(vRock).toFixed(1);
      const cyPlain = pgvToSvgY(vPlain).toFixed(1);

      if (cross) {
        cross.setAttribute('x1', cx);
        cross.setAttribute('x2', cx);
      }
      if (dotRock) {
        dotRock.setAttribute('cx', cx);
        dotRock.setAttribute('cy', cyRock);
      }
      if (dotPlain) {
        dotPlain.setAttribute('cx', cx);
        dotPlain.setAttribute('cy', cyPlain);
        dotPlain.style.display = showPlainEffect ? 'inline' : 'none';
      }

      const elMag = document.getElementById('readout-mag');
      const elRock = document.getElementById('readout-rock');
      const elPlain = document.getElementById('readout-plain');
      const elRatio = document.getElementById('readout-ratio');

      if (elMag) elMag.innerHTML = `<i>M</i><sub>L</sub> ${attenMag.toFixed(2)}`;
      if (elRock) elRock.textContent = `${vRock.toFixed(2)}×`;

      if (showPlainEffect) {
        const pct = Math.round(((vPlain / vRock) - 1) * 100);
        if (elPlain) elPlain.textContent = `${vPlain.toFixed(2)}×`;
        if (elRatio) elRatio.textContent = `平原強 +${pct}%`;
      } else {
        if (elPlain) elPlain.textContent = `未開啟`;
        if (elRatio) elRatio.textContent = `僅基準對照`;
      }
    }

    function setAttenPreset(mag) {
      attenMag = mag;
      const btnSmall = document.getElementById('btn-preset-small');
      const btnKh = document.getElementById('btn-preset-kh');
      const btnLarge = document.getElementById('btn-preset-large');

      [btnSmall, btnKh, btnLarge].forEach(function (b) {
        if (b) b.classList.remove('is-selected');
      });

      if (mag < 2.0 && btnSmall) btnSmall.classList.add('is-selected');
      else if (mag > 2.6 && btnLarge) btnLarge.classList.add('is-selected');
      else if (btnKh) btnKh.classList.add('is-selected');

      renderAttenuationChart();
    }

    function togglePlainCurve() {
      showPlainEffect = !showPlainEffect;
      const btn = document.getElementById('btn-toggle-plain-curve');
      if (btn) {
        if (showPlainEffect) {
          btn.classList.add('is-selected');
          btn.textContent = `已開啟：南線平原多重潛入波效應`;
        } else {
          btn.classList.remove('is-selected');
          btn.textContent = `已關閉：僅顯示岩盤基準`;
        }
      }
      renderAttenuationChart();
    }

    function updateDistanceReadout(val) {
      attenDist = Number(val);
      const label = document.getElementById('dist-label-val');
      if (label) {
        const zone = attenDist <= 15 ? `近場` : (attenDist <= 30 ? `中場` : `遠場`);
        label.textContent = `${attenDist} km（${zone}）`;
      }
      renderAttenuationChart();
    }

    // 4. Section 07: Interactive Concept Check Quiz
    const quizData = [
      {
        q: `問題 1 / 3：為何在相同體波規模 mb 下，地下核試爆的表面波規模 Ms 通常顯著低於天然地震？`,
        options: [
          `A. 地下爆炸由斷層剪切錯動主導，使體波完全消失`,
          `B. 地下爆炸為瞬間向外球形膨脹，能量高度集中於高頻體波，較少激發低頻表面波`,
          `C. 地下爆炸必定發生在超過 100 公里的深部地函中`
        ],
        correct: 1,
        explanation: `正確。天然地震因斷層剪切錯動產生強大的表面波；地下爆炸則是球形向外膨脹，能量集中於高頻體波，故相同 mb 下 Ms 明顯偏低。`
      },
      {
        q: `問題 2 / 3：TAIGER 計畫的 10 次人工井穴爆破相較於天然地震，在建立近地表 PGV 衰減關係式時最大的優勢為何？`,
        options: [
          `A. 爆破發震時刻、位置與炸藥量皆精確已知，可排除震源參數的不確定性`,
          `B. 人工爆破的震源深度比天然地震更深，能穿透整個地核`,
          `C. 人工爆破不會受到地質構造與測站距離的影響`
        ],
        correct: 0,
        explanation: `正確。人工井穴爆破精確掌握時間、座標與炸藥當量，彌補天然地震震源反演不確定性高的限制，並成功推估 2014 高雄氣爆規模約為 ML 2.38。`
      },
      {
        q: `問題 3 / 3：南線的觀測結果為何顯示「不可直接將山區岩盤的衰減公式套用於台灣西部平原」？`,
        options: [
          `A. 因為西部平原完全沒有地震測站可供觀測`,
          `B. 因為西部平原與麓山帶淺層速度梯度陡峭，造成多重潛入波使近場地動強於岩盤預期`,
          `C. 因為西部平原的震波衰減速度比山區岩盤快上十倍，沒有災害風險`
        ],
        correct: 1,
        explanation: `正確。淺層陡峭速度梯度引發多重潛入波，導致近場地動比岩盤預期更強；考量人口與產業集中於西部平原，未來必須建立平原專屬的衰減方程式。`
      }
    ];

    let currentQuizIdx = 0;

    function renderQuiz() {
      const item = quizData[currentQuizIdx];
      const qText = document.getElementById('quiz-question-text');
      const optBox = document.getElementById('quiz-options-container');
      const fb = document.getElementById('quiz-feedback');
      const nextBtn = document.getElementById('btn-quiz-next');

      if (qText) qText.textContent = item.q;
      if (fb) {
        fb.classList.remove('is-visible', 'is-correct', 'is-wrong');
        fb.textContent = ``;
      }
      if (optBox) {
        optBox.innerHTML = item.options
          .map(function (text, idx) {
            return `<button type="button" class="quiz-opt" onclick="answerQuiz(${idx})">${text}</button>`;
          })
          .join('');
      }
      if (nextBtn) {
        const nextNum = ((currentQuizIdx + 1) % quizData.length) + 1;
        nextBtn.textContent = `下一題（${nextNum} / ${quizData.length}）`;
      }
    }

    function answerQuiz(idx) {
      const item = quizData[currentQuizIdx];
      const optBtns = document.querySelectorAll('#quiz-options-container .quiz-opt');
      const fb = document.getElementById('quiz-feedback');

      optBtns.forEach(function (btn, bIdx) {
        if (bIdx === idx) btn.classList.add('is-chosen');
        else btn.classList.remove('is-chosen');
      });

      if (fb) {
        fb.classList.add('is-visible');
        if (idx === item.correct) {
          fb.classList.remove('is-wrong');
          fb.classList.add('is-correct');
          fb.textContent = item.explanation;
        } else {
          fb.classList.remove('is-correct');
          fb.classList.add('is-wrong');
          fb.textContent = `再試一次：請回顧演講紀錄中關於震源物理機制、TAIGER 井穴爆破與南線淺層速度梯度的說明。`;
        }
      }
    }

    function nextQuizQuestion() {
      currentQuizIdx = (currentQuizIdx + 1) % quizData.length;
      renderQuiz();
    }

    // Initialize interactive visuals on load
    document.addEventListener('DOMContentLoaded', function () {
      initScrollSpy();
      renderWaveforms();
      updateAzimuth(45);
      renderAttenuationChart();
      renderQuiz();
    });
  </script>
</body>
</html>
