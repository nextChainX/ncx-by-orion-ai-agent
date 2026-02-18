<p align="center">
  <img src="https://orion-production-agent.s3.us-east-1.amazonaws.com/media/logo.svg" alt="Orion AI Agent" width="72" />
</p>

<h1 align="center">Orion AI Agent</h1>

<p align="center">
  Enterprise AI customer support, booking, lead capture, and workflow automation widget.
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@nextchainx/orion-ai-agent"><img src="https://img.shields.io/npm/v/@nextchainx/orion-ai-agent.svg?style=flat-square&color=0066FF" alt="npm version" /></a>
  <a href="https://www.npmjs.com/package/@nextchainx/orion-ai-agent"><img src="https://img.shields.io/npm/dm/@nextchainx/orion-ai-agent.svg?style=flat-square" alt="downloads" /></a>
  <a href="#license"><img src="https://img.shields.io/badge/license-proprietary-333.svg?style=flat-square" alt="license" /></a>
  <a href="https://orion.nextchainx.io"><img src="https://img.shields.io/badge/product-Orion_AI-0066FF.svg?style=flat-square" alt="product page" /></a>
</p>

<p align="center">
  <a href="https://orion.nextchainx.io"><strong>Product Page →</strong></a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="https://nextchainx.io">Website</a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="mailto:official@nextchainx.io">Contact Sales</a>
</p>

---

## Overview

Orion AI Agent is a production-ready conversational AI system purpose-built for service businesses. It operates as a **digital receptionist**, **booking manager**, **lead capture engine**, **support desk**, and **CRM collector** — all inside one embeddable interface.

Drop it into any website or web application using a **React component** or a single **CDN script tag**. Configuration is driven by your Orion dashboard and can be overridden locally via props or options.

> **To activate Orion on your site, you need a valid `appId`.** Contact **[NextChainX](mailto:official@nextchainx.io)** or visit **[orion.nextchainx.io](https://orion.nextchainx.io)** to get started.

---

## Table of Contents

- [Overview](#overview)
- [Key Capabilities](#key-capabilities)
- [Installation](#installation)
- [Quick Start — React](#quick-start--react)
- [Quick Start — CDN (Plain HTML)](#quick-start--cdn-plain-html)
- [Configuration Reference](#configuration-reference)
- [Display Modes](#display-modes)
- [Lead Capture & Customer Info Collection](#lead-capture--customer-info-collection)
- [Appointment Booking](#appointment-booking)
- [Callbacks & Events](#callbacks--events)
- [Use Cases](#use-cases)
- [Getting Your App ID](#getting-your-app-id)
- [Requirements](#requirements)
- [Browser Support](#browser-support)
- [FAQ](#faq)
- [Support](#support)
- [License](#license)

---

## Key Capabilities

| Capability | Description |
|:-----------|:------------|
| **AI-Powered Conversations** | Natural language understanding that handles queries, qualifies leads, and resolves tickets autonomously. |
| **Lead Capture** | Built-in info collector gathers name, email, phone, and custom fields — before or during the conversation. |
| **Appointment Booking** | Real-time scheduling integrated into the chat flow. Customers book without leaving the widget. |
| **CRM Data Collection** | Automatically structures interaction data and syncs to your pipeline. |
| **Automated Follow-Ups** | Post-conversation actions, reminders, and notifications triggered by AI. |
| **Multi-Display Modes** | Floating bubble, left panel, right panel, or full modal — adapts to your layout. |
| **Full Theming** | Colors, logos, dark/light modes, positioning, and sizing — all configurable. |
| **React + CDN** | First-class React component *and* a zero-dependency CDN bundle with React included. |

---

## Installation

### NPM

```bash
npm install @nextchainx/orion-ai-agent
```

### Yarn

```bash
yarn add @nextchainx/orion-ai-agent
```

### pnpm

```bash
pnpm add @nextchainx/orion-ai-agent
```

---

## Quick Start — React

### Basic

```jsx
import { ChatWidget } from "@nextchainx/orion-ai-agent";

export default function App() {
  return <ChatWidget appId="your-app-id" />;
}
```

### With Branding & Overrides

Props passed locally always override dashboard/API configuration values.

```jsx
import { ChatWidget } from "@nextchainx/orion-ai-agent";

export default function App() {
  return (
    <ChatWidget
      appId="your-app-id"
      title="Acme Support"
      subtitle="We typically reply in under a minute"
      theme="dark"
      primaryColor="#6C63FF"
      position="bottom-left"
      floatingText="Chat with us"
      showTimestamp={true}
      customerInfoCollector={true}
    />
  );
}
```

### With Event Handlers

```jsx
import { ChatWidget } from "@nextchainx/orion-ai-agent";

export default function App() {
  const handleMessage = (message) => {
    console.log("Assistant responded:", message);
  };

  return (
    <ChatWidget
      appId="your-app-id"
      onOpen={() => console.log("Widget opened")}
      onClose={() => console.log("Widget closed")}
      onMessage={handleMessage}
    />
  );
}
```

### Panel Mode (Always Visible)

```jsx
<ChatWidget appId="your-app-id" displayMode="panel-left" />
```

### Modal Mode

```jsx
<ChatWidget appId="your-app-id" displayMode="modal" />
```

---

## Quick Start — CDN (Plain HTML)

No build tools, no framework. React and ReactDOM are bundled inside the CDN build.

### 1 — Add the Script

```html
<script src="https://cdn.jsdelivr.net/npm/@nextchainx/orion-ai-agent@1.0.3/dist/cdn.min.js"></script>
```

### 2 — Initialize

```html
<script>
  OrionAgent.init({ appId: "your-app-id" });
</script>
```

### 3 — Full Page Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>My Website</title>
</head>
<body>

  <h1>Welcome to My Business</h1>

  <script src="https://cdn.jsdelivr.net/npm/@nextchainx/orion-ai-agent@1.0.3/dist/cdn.min.js"></script>
  <script>
    OrionAgent.init({
      appId: "your-app-id",
      theme: "light",
      primaryColor: "#0066FF",
      position: "bottom-right",
      floatingText: "Need help?",
      customerInfoCollector: true,
    });
  </script>

</body>
</html>
```

### CDN API Methods

| Method | Description |
|:-------|:------------|
| `OrionAgent.init({ appId, ...options })` | Mount the widget with configuration |
| `OrionAgent.update({ ...options })` | Re-render with updated options |
| `OrionAgent.destroy()` | Unmount and fully remove the widget |

---

## Configuration Reference

### Required

| Prop | Type | Description |
|:-----|:-----|:------------|
| **`appId`** | `string` | **Required.** Your unique Orion business/app identifier. Contact **[NextChainX](mailto:official@nextchainx.io)** or visit **[orion.nextchainx.io](https://orion.nextchainx.io)** to obtain your **`appId`**. |

### Branding & UI

| Prop | Type | Description |
|:-----|:-----|:------------|
| `title` | `string` | Header title displayed at the top of the widget |
| `subtitle` | `string` | Secondary text shown beneath the title |
| `logo` | `string` | URL to your brand logo image |
| `primaryColor` | `string` | Main accent color (hex, rgb, hsl) |
| `theme` | `"light"` \| `"dark"` | Widget color scheme |
| `floatingBgColor` | `string` | Background color of the floating trigger button |
| `textColor` | `string` | Primary text color inside the widget |
| `floatingText` | `string` | Label displayed next to the floating icon when the widget is closed |

### Placement & Sizing

| Prop | Type | Default | Description |
|:-----|:-----|:--------|:------------|
| `position` | `"bottom-right"` \| `"bottom-left"` \| `"top-right"` \| `"top-left"` | `"bottom-right"` | Screen position of the widget |
| `buttonSize` | `number` | `56` | Floating button diameter in pixels |
| `zIndex` | `number` | `9999` | CSS z-index stacking order |

### Input & Message UI

| Prop | Type | Default | Description |
|:-----|:-----|:--------|:------------|
| `placeholder` | `string` | `"Type a message…"` | Placeholder text in the input field |
| `showTimestamp` | `boolean` | `false` | Display timestamps on each message |

### Toggles & Behavior

| Prop | Type | Default | Description |
|:-----|:-----|:--------|:------------|
| `showNotificationDot` | `boolean` | `true` | Show a notification indicator before the widget is first opened |
| `customerInfoCollector` | `boolean` | `false` | Enable the lead capture form that appears before chat begins |
| `displayMode` | `"floating"` \| `"panel-left"` \| `"panel-right"` \| `"modal"` | `"floating"` | Widget display mode (see [Display Modes](#display-modes)) |

---

## Display Modes

Orion supports four distinct display modes to fit different page layouts and UX requirements.

| Mode | Behavior |
|:-----|:---------|
| **`floating`** | Corner-positioned chat window with wave border. Click the bubble to toggle open/close. |
| **`panel-left`** | Full-height sidebar that slides in from the left edge of the viewport. |
| **`panel-right`** | Full-height sidebar that slides in from the right edge of the viewport. |
| **`modal`** | Centered overlay with blurred backdrop and wave border. |

### Usage Examples

**React:**

```jsx
// Floating (default)
<ChatWidget appId="your-app-id" displayMode="floating" />

// Left panel
<ChatWidget appId="your-app-id" displayMode="panel-left" />

// Right panel
<ChatWidget appId="your-app-id" displayMode="panel-right" />

// Modal
<ChatWidget appId="your-app-id" displayMode="modal" />
```

**CDN:**

```js
// Initialize with a mode
OrionAgent.init({ appId: "your-app-id", displayMode: "panel-right" });

// Switch modes at runtime
OrionAgent.update({ displayMode: "modal" });
```

---

## Lead Capture & Customer Info Collection

Enable `customerInfoCollector` to present a structured intake form before the conversation begins. This captures visitor information and feeds it directly into your pipeline.

```jsx
<ChatWidget
  appId="your-app-id"
  customerInfoCollector={true}
/>
```

**What it collects:**

- **Name** (required)
- **Email**, **Phone**, and any additional custom fields configured in your Orion dashboard

**How it works:**

1. Visitor opens the widget and sees the info collection form.
2. After submitting, the AI conversation begins with full context about the visitor.
3. Collected data is automatically synced to your CRM and linked to the conversation transcript.

**Ideal for:**

- Pre-qualifying leads before they engage with AI
- Capturing contact information for sales follow-up
- Routing conversations based on customer segment or intent
- Building your pipeline passively around the clock

---

## Appointment Booking

Orion handles real-time appointment scheduling directly within the chat flow. Customers can browse available slots, select a date and time, and confirm their booking — all without leaving the widget.

Booking configuration is managed through your **Orion dashboard**, including:

- Available services and session durations
- Business hours and availability windows
- Confirmation messages and reminders
- Calendar integrations (Google Calendar, Outlook, and more)

No additional code or props are required. Once booking is enabled in your dashboard, the AI agent handles scheduling as a natural part of the conversation.

---

## Callbacks & Events

Use callbacks to integrate Orion with your application logic — analytics, state management, CRM triggers, or custom workflows.

| Prop | Type | Triggered When |
|:-----|:-----|:---------------|
| `onOpen` | `() => void` | The widget opens |
| `onClose` | `() => void` | The widget closes |
| `onMessage` | `(message) => void` | The assistant sends a final response message |

### Example — Analytics Integration

```jsx
<ChatWidget
  appId="your-app-id"
  onOpen={() => analytics.track("orion_widget_opened")}
  onClose={() => analytics.track("orion_widget_closed")}
  onMessage={(msg) => analytics.track("orion_message_received", { message: msg })}
/>
```

---

## Use Cases

| Scenario | How Orion Handles It |
|:---------|:---------------------|
| **Missed calls** | AI answers instantly, 24/7 — no more voicemail backlogs |
| **Delayed WhatsApp replies** | Immediate automated responses with full business context |
| **Manual scheduling** | Real-time booking embedded directly in the chat widget |
| **Fragmented support channels** | One widget replaces email, phone, forms, and live chat |
| **Lead qualification** | Collects info, qualifies intent, and routes to your team |
| **Service inquiries** | Delivers accurate answers from your configured knowledge base |
| **Post-interaction follow-ups** | Automated reminders, confirmations, and re-engagement triggers |
| **CRM data entry** | Structured conversation data flows into your pipeline automatically |

---

## Getting Your App ID

> **`appId` is required** to activate Orion AI Agent on your website. Without a valid **`appId`**, the widget will not initialize.

To obtain your **`appId`**, contact the **NextChainX** team or sign up through the Orion product page:

| Channel | Link |
|:--------|:-----|
| 🚀 **Product Page** | **[orion.nextchainx.io](https://orion.nextchainx.io)** |
| 🌐 **Website** | [nextchainx.io](https://nextchainx.io) |
| ✉️ **Email** | [official@nextchainx.io](mailto:official@nextchainx.io) |

---

## Requirements

### React (NPM)

| Requirement | Version / Details |
|:------------|:------------------|
| React | `>= 17` |
| ReactDOM | `>= 17` |
| **`appId`** | Required — obtain from **[NextChainX](https://orion.nextchainx.io)** |
| Backend | Must be reachable at the configured base URL |

### CDN

| Requirement | Details |
|:------------|:--------|
| **`appId`** | Required — obtain from **[NextChainX](https://orion.nextchainx.io)** |
| Dependencies | None — React and ReactDOM are bundled in the CDN build |
| Backend | Must be reachable at the configured base URL |

---

## Browser Support

| Browser | Support |
|:--------|:--------|
| Chrome | ✅ Latest 2 versions |
| Firefox | ✅ Latest 2 versions |
| Safari | ✅ Latest 2 versions |
| Edge | ✅ Latest 2 versions |
| Mobile Safari (iOS) | ✅ |
| Chrome Mobile (Android) | ✅ |
| Samsung Internet | ✅ |

---

## FAQ

<details>
<summary><strong>How do I get an <code>appId</code>?</strong></summary>
<br />
Contact <strong><a href="mailto:official@nextchainx.io">NextChainX</a></strong> or visit <strong><a href="https://orion.nextchainx.io">orion.nextchainx.io</a></strong> to register your business and receive your unique <strong><code>appId</code></strong>.
</details>

<details>
<summary><strong>Does the CDN bundle include React?</strong></summary>
<br />
Yes. The CDN build bundles React and ReactDOM internally. No additional script tags or dependencies are needed.
</details>

<details>
<summary><strong>Can I override dashboard settings with local props?</strong></summary>
<br />
Yes. Any prop passed directly to <code>&lt;ChatWidget /&gt;</code> or <code>OrionAgent.init()</code> takes priority over the corresponding value from your Orion dashboard configuration.
</details>

<details>
<summary><strong>Does Orion work with Next.js, Remix, Nuxt, or Vite?</strong></summary>
<br />
Yes. The React component is compatible with any React-based framework. For SSR frameworks (Next.js, Remix), render the widget on the client side using dynamic imports or <code>useEffect</code>.
</details>

<details>
<summary><strong>Is the widget mobile-responsive?</strong></summary>
<br />
Yes. Orion adapts to all screen sizes and works seamlessly on both desktop and mobile browsers.
</details>

<details>
<summary><strong>Can I switch display modes at runtime?</strong></summary>
<br />
Yes. Use <code>OrionAgent.update({ displayMode: "modal" })</code> via CDN, or update the <code>displayMode</code> prop in React to switch modes dynamically.
</details>

<details>
<summary><strong>What is the difference between <code>panel-left</code> and <code>panel-right</code>?</strong></summary>
<br />
Both render a full-height sidebar. <code>panel-left</code> slides in from the left edge of the viewport, while <code>panel-right</code> slides in from the right. Choose based on your page layout and navigation placement.
</details>

<details>
<summary><strong>How is customer data handled?</strong></summary>
<br />
All data is transmitted securely and stored according to your Orion dashboard configuration. Contact <strong><a href="mailto:official@nextchainx.io">NextChainX</a></strong> for details on data processing, retention policies, and compliance.
</details>

---

## Support

Need help integrating or have questions about your deployment?

| Channel | Link |
|:--------|:-----|
| ✉️ **Email** | [official@nextchainx.io](mailto:official@nextchainx.io) |
| 🚀 **Product Page** | [orion.nextchainx.io](https://orion.nextchainx.io) |
| 🌐 **Website** | [nextchainx.io](https://nextchainx.io) |

---

## License

**Orion AI Agent** is a commercial product offered by **[NextChainX](https://nextchainx.io)**. All rights reserved.

See [LICENSE](./LICENSE) for full terms.

---

<p align="center">
  <sub>Built with precision by <a href="https://nextchainx.io"><strong>NextChainX</strong></a></sub>
</p>
