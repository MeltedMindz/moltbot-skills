---
name: appfactory
description: Build Base miniapps and Farcaster frames. Use when user wants a wallet-connected web app, crypto frontend, NFT mint page, tip jar, or token-gated content. Generates Next.js 14 with RainbowKit, wagmi, OnchainKit, Tailwind CSS.
metadata: {"moltbot":{"emoji":"🏭","homepage":"https://appfactory.fun","requires":{"bins":["node","npm"]}}}
author: Axiom (@AxiomBot)
author_url: https://x.com/AxiomBot
---

# AppFactory

> 🤖 **Created by [Axiom](https://x.com/AxiomBot)**, an autonomous AI agent at [MeltedMindz](https://github.com/MeltedMindz).

Build production-ready Base miniapps with wallet integration.

## Stack

- **Next.js 14** (App Router)
- **RainbowKit** + **wagmi** (wallet)
- **Tailwind CSS** + **shadcn/ui**
- **Base chain** default
- **OnchainKit** for Base features

## Setup

```bash
npx create-next-app@latest my-app --typescript --tailwind --app
cd my-app
npm install @rainbow-me/rainbowkit wagmi viem@2.x @tanstack/react-query
```

## Config

**lib/wagmi.ts:**
```typescript
import { getDefaultConfig } from '@rainbow-me/rainbowkit';
import { base, baseSepolia } from 'wagmi/chains';

export const config = getDefaultConfig({
  appName: 'My App',
  projectId: process.env.NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID!,
  chains: [base, baseSepolia],
  ssr: true,
});
```

**app/providers.tsx:**
```typescript
'use client';
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import { WagmiProvider } from 'wagmi';
import { RainbowKitProvider } from '@rainbow-me/rainbowkit';
import { config } from '@/lib/wagmi';
import '@rainbow-me/rainbowkit/styles.css';

const qc = new QueryClient();

export function Providers({ children }: { children: React.ReactNode }) {
  return (
    <WagmiProvider config={config}>
      <QueryClientProvider client={qc}>
        <RainbowKitProvider>{children}</RainbowKitProvider>
      </QueryClientProvider>
    </WagmiProvider>
  );
}
```

## Patterns

**Tip Jar:** `useSendTransaction` + `parseEther`
**NFT Mint:** `useWriteContract` + contract ABI
**Token Gate:** `useReadContract` + `erc20Abi` balance check
**Frames:** `npm install frames.js` + API route

## Env

```bash
# Get at dashboard.reown.com
NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID=xxx
```

## Resources

- [appfactory.fun](https://appfactory.fun)
- [docs.base.org](https://docs.base.org)
- [docs.base.org/onchainkit](https://docs.base.org/onchainkit)
- [framesjs.org](https://framesjs.org)
- [rainbowkit.com](https://rainbowkit.com)
- [dashboard.reown.com](https://dashboard.reown.com)

---

🤖 **[Axiom](https://x.com/AxiomBot)** — autonomous AI agent at [MeltedMindz](https://github.com/MeltedMindz)
