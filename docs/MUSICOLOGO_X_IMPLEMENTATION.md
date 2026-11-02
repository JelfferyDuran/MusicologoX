# Musicólogo X — Audio Foundation Plan

Status: planning only. No deployment or production changes.

## Product direction
Dominican street car-audio interface with customizable SUVs and a prominent working equalizer. Functionality first; no monetization work.

## Source audit (original project)
- React 19 + Vite + TypeScript; Capacitor Android support.
- Existing Web Audio EQ, analyser, compressor, synthetic bass, radio playlist, and soundboard.
- `src/components/AuthGate.tsx` stores passwords in localStorage and may register users during login. Never use it for Box OAuth or sensitive data.
- `src/utils/paidItems.ts` stores unlocks client-side; payment features are out of scope.
- `src/utils/audioEngine.ts` boosts gain aggressively. Audit clipping, bypass semantics, disconnected nodes, CORS handling, and audio graph lifecycle.
- Preserve MIT license and review SPDX header in App.tsx.

## Milestone 1: verifiable playback
1. Keep current UI functional while adding tests.
2. Verify local MP3/WAV import, pause/resume, next/previous, queue and error states.
3. Verify seven-band EQ audibly affects local audio, flat bypass is neutral, and clipping is controlled.
4. Check radio streams for availability, HTTPS, metadata, CORS, and EQ compatibility. Do not claim fallback until tested.
5. Test Chrome desktop, Safari iPhone, and Android Chrome; mark each test verified or unverified.

## Milestone 2: secure Box cloud
- Implement Box OAuth authorization code flow with PKCE where applicable, using a secure backend.
- Never put client secrets or long-lived tokens in frontend code, localStorage, GitHub, or chat.
- Backend handles scoped file listing and authorized playback access; allowlisted audio MIME types, range requests where supported, and token refresh.
- Tests: connect, browse, play, expire/reconnect, revoke, and logout.

## Milestone 3: visual and source expansion
- Equalizer as primary UI, SUV/chuchero customization, saved configurations.
- Dominican radio directory with health checks and verified backups.
- Spotify/Apple Music only through approved APIs and allowed playback; do not promise custom EQ for protected streams.
- PWA first, then mobile native capabilities and browser-extension companion.

## Definition of done
A feature is done only when implemented, tested, and verified on a named device. No fake audio visualizers, placeholder integrations, public deployment, or payment system.

## Immediate next actions
- Confirm repo visibility (currently public) and make private if intended.
- Audit and run baseline build locally or in CI before changing production code.
- Build a regression checklist, then implement audio graph safety and source adapter interfaces in this development branch.
