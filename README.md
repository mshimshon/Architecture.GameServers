# Project Checklist

## 1. Core Infrastructure Setup

- [ ] Configure Proxmox API access (tokens + roles)
- [ ] Test `pct create` workflow
- [ ] Test `pct exec` for package installation
- [ ] Test `pct push` for file provisioning
- [ ] Generate automation SSH keypair or SSH-CA
- [ ] Validate enabling SSH inside fresh Debian LXC
- [ ] Validate automation SSH access as `gsadmin`

---

## 2. GSM Game Module Development

- [ ] Create GSM module base folder structure
- [ ] Implement `install.sh` template
- [ ] Implement `start.sh` template
- [ ] Implement `stop.sh` template
- [ ] Implement `update.sh` template
- [ ] Create `game.json` template
- [ ] Test full GSM install flow for Project Zomboid
- [ ] Add second game module (Valheim or Rust)

---

## 3. Webmin GSM Control Module

- [ ] Create Webmin module directory structure
- [ ] Implement `index.cgi` (dashboard)
- [ ] Implement GSM command handlers (`actions.cgi`)
- [ ] Add Start/Stop/Restart/Update buttons
- [ ] Integrate GSM log viewer in Webmin
- [ ] Add config editor (Webmin file editor integration)
- [ ] Add ACL restrictions per client user
- [ ] Reload Webmin + validate module integration

---

## 4. Strapi Backend Setup

- [ ] Create Strapi Collections: Client, Game, GameServer
- [ ] Add fields: ip_address, ports, status, container_id, webmin_url
- [ ] Implement internal fields (`private: true`) for secrets
- [ ] Create API endpoint for provisioning worker
- [ ] Integrate SSH-cert/SSH-key provisioning model
- [ ] Add lifecycle hook to sanitize fields
- [ ] Test GameServer creation → API event flow

---

## 5. Provisioning Worker

- [ ] Implement Strapi → Worker event receiver
- [ ] Add Proxmox API “create container” logic
- [ ] Implement container bootstrap via `pct exec`
- [ ] Enable SSH inside container
- [ ] Create automation user (`gsadmin`)
- [ ] Inject automation SSH public key
- [ ] Install Webmin via automation script
- [ ] Install GSM via automation script
- [ ] Push GSM game modules into container
- [ ] Run GSM game install (SteamCMD)
- [ ] Create Webmin client user
- [ ] Apply Webmin ACL restrictions
- [ ] Update Strapi with final server status + URLs
- [ ] Implement error-handling + fallback cleanup

---

## 6. Integration Testing

- [ ] Test full workflow: Strapi → Worker → Proxmox → Webmin
- [ ] Test multi-game install support
- [ ] Validate ports are correctly assigned
- [ ] Validate Webmin login + user isolation
- [ ] Validate GSM Start/Stop/Restart/Update commands
- [ ] Validate logs + config editing
- [ ] Validate SSH automation post-bootstrap
- [ ] Fix race conditions / timing issues

---

## 7. Deployment + Hardening

- [ ] Connect port registry system with Proxmox firewall rules
- [ ] Implement nightly backup job (game data + configs)
- [ ] Implement restore procedure
- [ ] Add ActivePieces integration (notifications + hooks)
- [ ] Configure TLS and reverse proxy for Webmin
- [ ] Validate no passwords stored in plaintext anywhere
- [ ] Validate workers use SSH keys/certificates exclusively
- [ ] Final security audit (permissions, ACL, SSH)

