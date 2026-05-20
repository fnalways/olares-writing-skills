# Olares Wordlist

A–Z reference for word and phrase usage in Olares UI.

## How to use

This wordlist captures words and phrases that are commonly misused, ambiguous, or translated literally from Chinese. It complements the [UX Writing Guidelines](ux-writing-guidelines.md) and the [Localization Glossary](glossary.md).

- **Wordlist (this file)**: how to use individual words in source English. "Use this word, not that one."
- **UX Writing Guidelines**: rules for tone, structure, and patterns.
- **Glossary**: how each term should be translated into target languages.

When in doubt, default to the simpler, more common word. If you're translating from Chinese and a word feels like a direct rendering, check this list first.

---

## A

### a / an

Use `an` before words that begin with a vowel *sound*, not just a vowel letter.

❌ `a HTTP request`, `a URL`, `a email`  
✅ `an HTTP request`, `a URL`, `an email`

### abort

Don't use. Sounds harsh and clinical.

❌ `Abort the upload?`  
✅ `Cancel the upload?` / `Stop the upload?`

### above / below

Don't use as the only way to locate UI elements. Layout changes (responsive, RTL) make these references unreliable, and screen readers can't see the layout.

❌ `Click the button above to continue.`  
✅ `Click **Continue**.` / `In the previous step, you...`

### activate / deactivate

Don't use for toggles. Use `turn on` / `turn off`.

❌ `Activate dark mode`  
✅ `Turn on dark mode`

> **Exception** Use `activate` for one-time setup actions where a license, account, or device becomes operational: `Activate Olares`, `Activation required`.

### add

Use when bringing an existing object into a new context.

✅ `Add user` (the user already exists; you're adding them to a group)  
✅ `Add member` (existing person joining a workspace)

> Compare with **create** (make from scratch) and **new** (dialog title for "make from scratch").

### admin / administrator

Use `admin` as the standard short form, both as adjective (`admin password`, `admin privileges`, `admin tools`) and as a noun for the role (`Add an admin`). Don't use `administrator` in user-facing UI.

❌ `Administrator privileges are required.`  
✅ `Admin privileges are required.`

❌ `Administrator settings`  
✅ `Admin settings`

> **Exception** Keep `Administrator` only when it refers to a specific OS-level account name (Windows `Administrator`, the root account in admin docs) where renaming would be inaccurate.

### app / application

Use `app`. Never `application`.

❌ `Install the application`  
✅ `Install the app`

> **Exception** Keep `application` only when it's part of a fixed proper name or technical term where it can't be changed.

### assign / unassign

Use `assign` to give a permission, role, or item to someone. Don't pair with `unassign` — use `remove` instead.

✅ `Assign role`  
✅ `Remove role` (not `Unassign role`)

### assist / assistance

Don't use. Use `help`.

❌ `Need assistance? Contact support.`  
✅ `Need help? Contact support.`

❌ `Wise will assist you with translation.`  
✅ `Wise helps you translate content.`

> **Exception** `assistive technology` is the established accessibility term — don't rephrase it.

### attempt

Don't use as a verb. Use `try`.

❌ `Wise will attempt to retrieve the page.`  
✅ `Wise tries to retrieve the page.`

> Keep the noun `attempt` only when it's part of a domain term — for example, `login attempts` or `sign-in attempts` in security and audit contexts.

### authentication / authorization

Don't conflate. Authentication = proving who you are. Authorization = what you're allowed to do.

✅ `Authentication failed.` (login problem)  
✅ `You're not authorized to view this folder.` (permission problem)

---

## B

### brand names and proper nouns

Brand names, product names, and third-party service names keep their official capitalization in both English and Chinese UI. Sentence-case rules don't apply to them, and linters that flag them are reporting false positives.

**Olares brand terms** (stay in English in all languages):
`Olares`, `Olares OS`, `Olares ID`, `Olares Space`, `LarePass`, `Vault`, `Profile`, `Studio`, `Wise`

**Built-in Olares apps** (translate per target language; English keeps initial capital):
`Desktop`, `Market`, `Files` (中文 `文件管理器`), `Settings`, `Control Hub`, `Dashboard`

**Third-party services** (keep official spelling, not sentence-cased):
`AWS S3`, `Amazon S3`, `Tencent COS`, `Google Drive`, `iCloud`, `GitHub`, `WeChat`

❌ `From aws s3` / `From Aws s3` (linter wants sentence case)  
✅ `From AWS S3`

❌ `From tencent cos`  
✅ `From Tencent COS`

❌ `Back up to olares space`  
✅ `Back up to Olares Space`

When a sentence-case linter flags any of the above, ignore it. Do not lowercase brand or service names to satisfy the rule.

### back-end / backend

Write `back-end` (adjective) and `back end` (noun). Don't write `backend`.

❌ `backend service`  
✅ `back-end service`

### below

See [above / below](#above--below).

### bind / bound / unbind

**Don't use.** This is a direct rendering of Chinese 绑定/解绑. In English UI, things are *created*, *connected*, *linked*, *paired*, *attached*, or *associated* — not bound.

#### General mapping

| 场景 | ❌ 不使用 | ✅ 使用 |
|------|---------|--------|
| 关联账号 | Bind your phone number | Link your phone number / Add your phone number |
| 关联设备 | Bind device | Pair device / Connect device |
| 关联钱包 | Bind wallet | Connect wallet |
| 解除关联 | Unbind email | Remove email / Unlink email / Disconnect email |
| 成功 toast | Bound / Bind successful | Linked / Connected / Paired |
| 失败 toast | Bind failed | Unable to link / Unable to connect |

#### Pick the verb by relationship type

Match the verb to the **nature of the relationship**, not to the Chinese 绑定. Use this table to pick the right one for Olares-specific objects:

| 关系类型 | EN verb pair | 中文 | Olares 场景示例 |
|---------|--------------|------|---------------|
| **Permanent registration** (one-way, no undo) | `create` | 创建 | DID → Olares ID |
| **Account / identity association** (reversible) | `link` / `unlink`(or `add` / `remove`) | 关联 / 解除关联(或 添加 / 移除) | Olares Space 账号、邮箱、手机号、社交账号 / VC、组织域名 |
| **Network / service session** (reversible, runtime) | `connect` / `disconnect` | 连接 / 断开连接 | 区块链钱包(MetaMask)、远程服务器、Wi-Fi、第三方账户授权 |
| **Device pairing** (reversible, hardware) | `pair` / `unpair` | 配对 / 取消配对 | 蓝牙设备、近场设备 |
| **Resource attachment** (reversible, runtime) | `attach` / `detach` | 关联 / 取消关联 | Studio 开发容器 ↔ 应用、卷 ↔ 工作负载 |
| **State assignment** (set a value, can clear) | `set` / `clear`(or `link` / `unlink`) | 设置 / 取消设置 | NFT 头像 → Olares ID、默认域名 |

If you're not sure which row applies, ask: *Can the user undo this in the UI?*
- **No, ever** → `create` / `register`
- **Yes, at runtime** → `connect` / `disconnect`
- **Yes, by removing** → `link` / `unlink` or `add` / `remove`

#### Special case: DID ↔ Olares ID

The relationship between a DID and an Olares ID is a **one-way, permanent** registration — there is no "unbind" operation. Use `create` (中文 `创建`), not `link`. `link` implies a reversible connection, which would mislead users.

| 场景 | ❌ 不使用 | ✅ 使用 |
|------|---------|--------|
| 动作 / 按钮 | Bind Olares ID / Link Olares ID | **Create Olares ID** / 创建 Olares ID |
| 未创建 | No Olares ID linked / 未绑定 Olares ID | **No Olares ID yet** / 还没有 Olares ID |
| 该 DID 没有对应 Olares ID | This DID is not bound to any Olares ID | **No Olares ID created for this DID** / 当前 DID 还没有创建 Olares ID |
| 成功 toast | Bound / Linked | **Olares ID created** / 已创建 Olares ID |
| 失败 toast | Bind failed | **Unable to create Olares ID** / 无法创建 Olares ID |

> Don't mention "blockchain" in user-facing copy. The on-chain nature is an implementation detail — users only need to understand that an Olares ID is permanent and globally unique.

#### Technical-term exceptions (keep `bound` / `binding`)

These are established technical terms — don't translate them away:

| 上下文 | 保留写法 | 说明 |
|--------|---------|------|
| Kubernetes PV / PVC 状态 | `Bound` / `Binding` / `Unbound` | K8s 官方术语,出现在 Control Hub / Control Panel 等运维界面 |
| Volume binding mode | `Volume binding mode` / `Immediate binding` / `Delayed binding` | 同上 |
| 数学 / 逻辑 / 编程文档(如 "early binding") | `binding` | 学科术语 |

These appear in admin/devops surfaces where the audience is technical. Don't surface them in end-user UX copy.

### biometric / biometrics

`biometric` is the adjective. `biometrics` is the noun.

❌ `Scan your biometry to verify`  
✅ `Scan your biometrics to verify` (noun)  
✅ `Set up biometric authentication` (adjective)

### blacklist / whitelist

Don't use. Use `blocklist` / `allowlist`, or `denylist` / `safelist`.

### button

Don't include the word "button" when telling users to interact with one. Assistive technology already announces it.

❌ `Click the **Save** button.`  
✅ `Click **Save**.`

---

## C

### can / could / may / might

- `can` = ability
- `could` = past tense only (don't use as a softer "can")
- `may` = permission, or uncertainty (ambiguous — usually avoid)
- `might` = possibility

❌ `This site may limit access for anonymous users.` (ambiguous: permission or possibility?)  
✅ `This site might limit access for anonymous users.`

### cancel

Use to dismiss a dialog or stop an in-progress action.

✅ `Cancel` (button to close a dialog without saving)  
✅ `Cancel upload` (stop an ongoing upload)

Don't use `cancel` to mean `close` for a passive view. Use `Close` for windows, panels, or read-only views.

### can't / cannot

In **error messages**, use `cannot`. In all other contexts, `can't` is fine.

❌ `This operation can't be undone.` (in an error or warning)  
✅ `This operation cannot be undone.`  
✅ `You can't edit this file because it's locked.` (informational, not an error)

### check / uncheck

Don't use for checkboxes. Ambiguous — does "check" mean to verify, or to mark?

❌ `Check the **Auto-update** checkbox.`  
✅ `Select the **Auto-update** checkbox.` / `Clear the **Auto-update** checkbox.`

### click

Mouse-only. Use `select` for platform-neutral instructions. Use `click` only when the action is mouse-specific (e.g., "right-click").

❌ `Click **Save** to continue.`  
✅ `Select **Save** to continue.`

### close

Use for closing a window, dialog, panel, or view. Don't use as a synonym for `cancel`.

### configure

Avoid. Use `set up` (for initial setup) or `change settings`.

❌ `Configure the proxy server.`  
✅ `Set up the proxy server.` / `Change proxy settings.`

### confirm

Avoid as a button label. Use the specific action verb.

❌ `Confirm` (button)  
✅ `Save`, `Delete`, `Submit`, `Add`

> **Exception** "Confirm password" (input field label) is fine — it describes what's being entered.

### connect / disconnect

Use for network or device pairing. Pair with `disconnect`, not `unbind`.

✅ `Connect to Olares`  
✅ `Disconnect from server`

### contact us

Don't use. Be specific about the contact method.

❌ `Please contact us.`  
✅ `Email support@olares.com.` / `Open the help center.`

### create

Make a new object from scratch. Used as the confirm button in "New xxx" dialogs.

✅ Title: `New project` / Button: `Create`

> Compare with **add** (use existing) and **new** (dialog title).

---

## D

### data

Treat as singular in user-facing text.

✅ `Your data is encrypted at rest.`  
✗ `Your data are encrypted at rest.` (technically correct, but stilted)

### deactivate

See [activate](#activate--deactivate).

### delete

Permanent removal. Pair with `Cancel` in confirmation dialogs, never with `OK` or `Yes`.

✅ `Delete file?` → buttons: `Delete`, `Cancel`

> Compare with **remove** (take out of a list, but the object still exists in the system).

### desktop / mobile

Lowercase as adjectives describing form factor.

✅ `desktop browser`, `mobile app`

### dialog / dialogue

Use `dialog` (American spelling) when referring to UI windows.

✅ `Confirmation dialog`

### directory

For users, prefer `folder`. Use `directory` only in technical/CLI contexts where the term is well-established.

❌ `Create a new directory.` (general UI)  
✅ `Create a new folder.`

### disable / enable

Use for features and options. Pair correctly: `enable` ↔ `disable`.

✅ `Enable two-factor authentication`  
✅ `Disable notifications`

Don't use `disabled` to describe people — use `disability`-aware language. See [UX Writing Guidelines](ux-writing-guidelines.md#使用-people-first-表述).

### dismiss

Use for non-blocking notifications and toasts that the user wants to clear.

✅ `Dismiss` (close a banner)

### don't / do not

Use the contraction `don't` in friendly UI text. Use `Do not` only in serious warnings or in formal documents.

✅ `Don't show this again`  
✅ `Don't Save` (in unsaved-changes dialogs — this is a fixed pattern)

### download / upload

One word, no hyphen. Both verb and noun forms.

❌ `down-load`, `up-load`  
✅ `download`, `upload`

### drag / drag and drop

Use just `drag`. Don't say "drag and drop" — drop is implied.

❌ `Drag and drop the file here.`  
✅ `Drag the file here.`

---

## E

### e.g. / i.e.

Avoid in UI. Replace with `for example` and `that is` for clarity in translation.

❌ `Choose a region (e.g., us-west).`  
✅ `Choose a region, for example, us-west.`

### email

One word, no hyphen, lowercase except at the start of a sentence.

❌ `e-mail`, `Email address`  
✅ `email`, `email address`

### enable

See [disable / enable](#disable--enable).

### enter

Use for typing text into a field. Don't use `input` or `type`.

❌ `Input your password`  
✅ `Enter your password`

### erase

Don't use for digital deletion. Use `delete` or `clear`.

❌ `Erase history`  
✅ `Clear history` / `Delete history`

### error

Use for system-level problems (server timeout, crash). Always pair with a description that explains the cause or next action.

❌ `Network error.` (alone, with no context)  
✅ `Network error. Check your connection and try again.`

### etc.

Avoid. Either commit to listing the items or rewrite to omit the trailing "and so on."

❌ `Supports JPG, PNG, etc.`  
✅ `Supports JPG, PNG, and GIF.` / `Supports common image formats including JPG and PNG.`

### execute

Avoid. Use `run`.

❌ `Execute the script`  
✅ `Run the script`

### exit

Don't use as a button label. Use `Cancel`, `Close`, or `Sign out` depending on the context.

---

## F

### Face ID / Touch ID

Apple trademarks. Don't use across-platform.

❌ `Set up Face ID`  
✅ `Set up face authentication`  
✅ `Set up fingerprint`

### fail / failed / failure

In user-facing UI, prefer `Unable to + verb` over `Failed to + verb`. Reserve `failed` for the "Verb-ing failed" toast pattern when there's no object.

❌ `Failed to upload photo`  
✅ `Unable to upload photo`

✅ `Refresh failed` (no object — fine)

### feature

Use to describe product capabilities. Don't use `function` or `functionality` interchangeably.

❌ `This functionality requires a paid plan.`  
✅ `This feature requires a paid plan.`

### field

Use to refer to input fields when adding a descriptor would help (in tutorials or descriptions).

✅ `In the **Email** field, enter your address.`

But when telling users to interact with a labeled field, drop "field":

❌ `Click in the **Email** field and type.`  
✅ `Enter your email address.`

### file / folder

Use `folder` for collections of files (not `directory` in user-facing UI).

### finish

Final step button in a multi-step wizard. Don't use `Confirm` or `Done`.

❌ Wizard final button: `Confirm`  
✅ Wizard final button: `Finish`

### finished / done

When indicating completion, prefer specific past participles or "completed":

❌ `Done!` (toast after sync)  
✅ `Synced` / `Sync completed`

---

## G

### grant

Avoid for permission flows. Use `allow` instead.

❌ `Grant access to your camera?`  
✅ `Allow access to your camera?`

---

## H

### hang / hung / not responding

Don't say a system or app "hangs" or "is hung." Use "not responding" or "stopped responding."

❌ `The app hung.`  
✅ `The app stopped responding.`

### help

Lowercase in running text, capitalized when used as a navigation label or page title.

✅ `Need help?` / `Help center` / `Open Help`

### hide / show

Pair these as opposites for toggling visibility.

✅ `Show password` / `Hide password`

### home page / homepage

Use `home page` (two words) for the front page of a website. Use `homepage` only when referring to a browser's home page setting.

### host / hostname

Lowercase, one word for `hostname`.

---

## I

### info / information

Use `info` in compact UI elements (tooltips, labels, toasts). Use `information` in full sentences and formal copy.

✅ `Show info`, `View information about your account`

### input

Noun only. Don't use as a verb.

❌ `Please input server address`  
✅ `Enter the server address`  
✅ `Voice input`, `input method` (noun forms — fine)

### install / uninstall

Use for apps. Pair correctly. Don't use `set up` and `remove` as substitutes — these mean different things.

✅ `Install app` / `Uninstall app`

### invalid / incorrect

- `Invalid` = wrong format. Always include the expected format if you can.
- `Incorrect` = right format, wrong value.

❌ `Invalid password` (the format wasn't wrong; the value was)  
✅ `Incorrect password`

❌ `Invalid email format.` (no example)  
✅ `Invalid email format. Use name@example.com.`

---

## J

### just

Avoid as filler. Adds noise without meaning.

❌ `Just enter your email to continue.`  
✅ `Enter your email to continue.`

---

## K

### key

In security contexts, use `key` for cryptographic keys, `password` for user passwords, and `passphrase` only when specifically referring to longer multi-word secrets.

### kill

Don't use for processes or tasks. Use `stop`, `end`, `terminate`, or `close`.

❌ `Kill the process.`  
✅ `Stop the process.` / `End the task.`

---

## L

### launch

Avoid. Use `open` for apps and `start` for processes.

❌ `Launch the app.`  
✅ `Open the app.`

### LarePass

Olares companion app. Always written this way — never `Larepass`, `larepass`, or `LarPass`.

### legacy

Use neutrally to describe older systems still in use. Don't use as a euphemism for "deprecated" — say `deprecated` directly if that's what you mean.

### let / allow / enable

Prefer `let` (simpler).

❌ `Allow you to manage notifications.`  
✅ `Lets you manage notifications.`

### log in / log on / login / signin

- `log in`, `sign in` = verb (two words)
- `login`, `sign-in` = noun or adjective

❌ `Click here to login.`  
✅ `Click here to log in.`

❌ `Use your sign-in credentials.` (acceptable, but prefer simpler)  
✅ `Use your login.`

**Olares uses `sign in` / `sign out`** for all consumer-facing surfaces. Reserve `log in` / `log out` for technical or administrative contexts (e.g., system console, admin docs) where it matches platform conventions. Don't mix the two in the same surface.

### log out / sign out / logout

Same rule. `log out`, `sign out` (verb) / `logout`, `sign-out` (noun).

Olares uses **`sign out`** in consumer-facing UI. ✅ `Sign out` (button)

---

## M

### master / slave

Don't use. See [UX Writing Guidelines](ux-writing-guidelines.md#替换有历史包袱的技术术语) for replacements.

### may

See [can / could / may / might](#can--could--may--might).

### menu

Don't say "drop-down menu" — `menu` is enough. Reserve "drop-down" for the visual style of the picker if it matters.

### might

See [can / could / may / might](#can--could--may--might).

### modify

Avoid. Use `change` or `edit`.

❌ `Modify your profile.`  
✅ `Edit your profile.`

---

## N

### native

Avoid when describing features. Use `built-in`.

❌ `Native video editor`  
✅ `Built-in video editor`

> **OK** to use `native` for technical contexts: native app (vs. web app), native code.

### new

Used as a dialog title prefix for creation flows. Pair with `Create` or `Add` button.

✅ Title: `New folder` / Button: `Create` (or `Add`, depending on context)

> Compare with **create** (make from scratch) and **add** (use existing).

### normal

Don't use to contrast with `disabled` (in the disability sense). See [UX Writing Guidelines](ux-writing-guidelines.md#使用-people-first-表述).

### note / notes

Singular when adding a related note (`Add note` button, `Note` field). Plural when used as a tab, menu, header, or reference label (`Notes` tab).

---

## O

### OK / Cancel

Avoid `OK` as a button label except in pure information dialogs (`Got it`). Use specific action verbs.

❌ `Save changes? OK / Cancel`  
✅ `Save changes? Save / Cancel`

### one-time

Hyphenate as an adjective.

✅ `One-time password`

### online / offline

One word, no hyphen.

### open

Use for apps, files, panels, and dialogs.

✅ `Open Settings`, `Open the file`

### operation

In success/failure messages, prefer the specific action over the generic word "operation."

❌ `Operation failed.`  
✅ `Unable to save the file.`

> Acceptable in fixed phrases: `This operation cannot be undone.`

### option / preference

Use `option` for choices in a dropdown or radio group. Use `setting` for things stored in Settings. Don't use `preference` — it's reserved for macOS lingo.

---

## P

### password / passcode / PIN

- `password` = user-chosen secret string (any length).
- `passcode` = numeric code, often device-level (Apple convention).
- `PIN` = numeric code, typically 4–6 digits, all caps.

### permissions

Plural when listing or granting multiple. Singular when referring to a single permission.

✅ `Manage permissions`, `Camera permission required`

### Please

Use only when the system caused the problem, or when omitting it would sound abrupt. See [UX Writing Guidelines](ux-writing-guidelines.md#慎用-please-和-sorry).

### plug-in / plugin

Use `plug-in` (hyphenated).

❌ `plugin`  
✅ `plug-in`

### pop-up / popup

Use `pop-up` (hyphenated) as a noun and adjective.

### preference

See [option](#option--preference).

### previous

Don't use as a wizard navigation button. Use `Back`.

❌ Wizard buttons: `Previous` / `Next`  
✅ Wizard buttons: `Back` / `Next`

### proceed

Avoid. Use `continue`.

❌ `Proceed to checkout.`  
✅ `Continue to checkout.`

---

## Q

### quit

Avoid. Use `close` for apps, or `sign out` for sessions.

❌ `Quit the app.`  
✅ `Close the app.`

---

## R

### read-only / read only

Hyphenate as an adjective. Don't write `readonly`.

❌ `readonly`, `Read-Only`  
✅ `read-only` (sentence case)

### real-time / real time

`real-time` (hyphenated) as adjective. `in real time` (no hyphen) as adverb.

✅ `Real-time sync` (adjective)  
✅ `Sync in real time` (adverb)

### refresh

Use to reload data without leaving the page.

✅ `Refresh` / `Refreshed` (success toast) / `Refresh failed` (failure toast)

### remove

Take an item out of a list, group, or container. The item still exists somewhere in the system.

✅ `Remove user from group` (the user still has an account)

> Compare with **delete** (permanent destruction).

### restart

Use for restarting services, devices, or apps.

✅ `Restart Olares` / `Restart required`

### restore

Use for bringing something back from a backup or trash.

✅ `Restore from backup` / `Restore deleted file`

### retry

OK as a button label after a failure.

✅ `Retry` (button) / `Try again` (instruction in body text)

### right-click

Mouse-specific. Acceptable when the action is mouse-only. Otherwise prefer "open the context menu" or describe the keyboard alternative.

---

## S

### save

Persist changes to existing content. Pair with `Cancel`.

✅ Edit dialog buttons: `Save` / `Cancel`

> Don't use `Save` as the confirm button when creating something new — use `Create` or `Add` instead.

### select

Platform-neutral verb for clicking, tapping, or otherwise activating a UI element. Default to `select` over `click` and `tap`.

✅ `Select **Save** to continue.`

### set up / setup

`set up` (verb, two words). `setup` (noun).

❌ `Setup your account.` (verb, should be two words)  
✅ `Set up your account.`  
✅ `Initial setup` (noun, one word)

### settings

Capitalized when referring to the Settings app or page. Lowercase when referring to settings as a category in general.

✅ `Open **Settings**.` (the app/page)  
✅ `Change your network settings.` (general)

### sign in / sign out

See [log in](#log-in--log-on--login--signin).

### sorry

Use sparingly, and only when the system caused the problem. Never use to soften user-caused errors.

❌ `Sorry, your password is incorrect.` (user error — don't apologize)  
✅ `Incorrect password.`

❌ `Sorry, Wise can't save this page right now.`  
✅ `Wise cannot save this page because of the website's restrictions.`

### successfully / success

Don't add to success messages. The verb form already indicates success.

❌ `File uploaded successfully.`  
✅ `File uploaded.`

❌ `Bind successful`  
✅ `Linked` / `Connected`

### switch

Use for toggling between modes, views, or accounts.

✅ `Switch to grid view` / `Switch account`

> Don't confuse with the toggle component (which is operated with `turn on` / `turn off`).

### sync

Both verb and noun. Don't use `synchronize` or `synchronization` in UI.

❌ `Synchronize files`  
✅ `Sync files`

For repeated sync actions, use `resync` (verb), not `resynchronize`. Avoid the compound noun `re-sync` — rewrite as "sync again" instead.

❌ `Resynchronize files`  
✅ `Resync files` / `Sync files again`

---

## T

### tap

Touch-only. Use `select` instead unless the instruction is touch-specific.

❌ `Tap **Save**.`  
✅ `Select **Save**.`

### terminate

Avoid. Use `end` or `stop`.

### thank you

Don't use in transactional UI. Reserved for explicit moments of acknowledgment (e.g., onboarding completion, payment confirmation), and even then, use sparingly.

### that

Keep `that` as a conjunction. It helps translators parse clause structure.

❌ `Verify the account is active.`  
✅ `Verify that the account is active.`

### then

Use to chain steps in instructions. Avoid stacking too many "then"s.

✅ `Open Settings, then select Network.`

### tip / tips

Singular for individual tips. Plural for collections.

✅ `Tip: Hold Shift to select multiple files.`  
✅ `Tips and tricks` (page title)

> **Don't use** generic `Tips` or `Note` as a dialog header. Make the header specific to the task.

### touch ID

See [Face ID](#face-id--touch-id).

### try again

Use as instructional text in error messages. Use `Retry` as a button label.

✅ Body: `Check your connection and try again.`  
✅ Button: `Retry`

### turn on / turn off

For toggle switches. Don't use `activate` / `deactivate` or `enable` / `disable` for toggles.

❌ `Activate dark mode`  
✅ `Turn on dark mode`

---

## U

### unable to

Use in user-facing failure messages — softer than "Failed to."

✅ `Unable to connect to the server.`

### undo

Use to reverse the last action. Always pair with the original action's name where possible.

✅ `Undo delete` / `Folder deleted. Undo`

### uninstall

See [install](#install--uninstall).

### unlink / disconnect

Use to break an existing link or connection. Don't use `unbind`.

❌ `Unbind your wallet`  
✅ `Disconnect wallet` / `Unlink wallet`

### upload

See [download](#download--upload).

### URL / URLs

All caps. The plural is `URLs`, not `Urls`.

❌ `Url`, `urls`  
✅ `URL`, `URLs`

### user

Use `user` in technical or admin contexts. Use `you` when speaking to the user directly.

❌ `The user can change their password.` (when speaking to the user)  
✅ `You can change your password.`

✅ `Add user` (admin context — the admin is acting on a different user)

### username / user name

One word. Always `username`, never `user name` or `User name`.

❌ `User name is required.`  
❌ `Enter your User name`  
✅ `Username is required.`  
✅ `Enter your username`

> The placeholder convention `{username}` is one word for the same reason. Don't capitalize the variable form (`{Username}`) unless it's the first word in a sentence.

### utilize

Don't use. Use `use`.

❌ `Utilize this feature to...`  
✅ `Use this feature to...`

---

## V

### verify

Use when confirming identity or ownership. Specific and clear.

✅ `Verify your email address.`

> Compare with **confirm** (acknowledge a choice) and **check** (look at).

### via

Avoid in UI. Use `through`, `with`, or `by`.

❌ `Sign in via Google.`  
✅ `Sign in with Google.`

### view

OK as both noun and verb. Don't use `view` when `see` or `read` would be simpler.

❌ `View the terms of service.`  
✅ `Read the terms of service.`

---

## W

### we

Use sparingly. Reserve for system-initiated messages (status updates, errors) where Olares is the implicit speaker. Avoid in instructional content.

❌ `We recommend you set up two-factor authentication.`  
✅ `Set up two-factor authentication for extra security.`

### Wi-Fi

Always written `Wi-Fi`. Never `wifi`, `WiFi`, or `wi-fi`.

❌ `Connect to wifi.`  
✅ `Connect to Wi-Fi.`

### will

Avoid. Use simple present tense.

❌ `This will delete the file permanently.`  
✅ `This deletes the file permanently.` / `This action cannot be undone.`

### would

Avoid as a softener. Direct present tense is clearer.

❌ `Would you like to save?`  
✅ `Save changes?`

---

## Y

### you / your

Use to address the user directly. Default voice for instructional content.

❌ `The user must confirm their email.`  
✅ `Confirm your email.`

### you can

Often deletable filler. Cut it if possible.

❌ `You can drag the file to upload.`  
✅ `Drag the file to upload.`

---

## Numbers and symbols

### `&` (ampersand)

Don't use in UI text. Spell out "and." Screen readers may read `&` as "ampersand," and translators may handle it inconsistently.

❌ `Save & continue`  
✅ `Save and continue`

> **Exception** Acceptable in compact tabular UI where space is tight, but avoid when possible.

### `+` (plus sign)

Spell out as "plus" in instructions. OK as a button icon (the universal "add" symbol).

❌ `Press Cmd + S` (in body text — should describe in words)  
✅ `Press Command-S` / `Press Command and S together`

### `/` (slash)

Use without spaces around it. Don't overuse — slashes can be ambiguous to translate.

❌ `Richtext / Markdown`  
✅ `Richtext/Markdown`  
✅ Better: pick one term, or use "or": `Rich text or Markdown`

### `…` (ellipsis)

Use only to indicate an in-progress operation. Don't use in button or menu labels.

❌ `Save...` (button)  
✅ `Saving...` (toast)

An ellipsis at the end of an ongoing-operation label is **not** end punctuation. The "single-sentence UI values have no end punctuation" rule does not apply, and lint warnings that treat trailing `...` as a stray period are false positives.

✅ `Collecting...` / `正在收集...`  
✅ `Parsing content...` / `正在解析...`  
✅ `Uploading...` / `正在上传...`

---

## See also

- [UX Writing Guidelines](ux-writing-guidelines.md) — tone, structure, and patterns
- [UX Localization Guidelines](ux-localization-guidelines.md) — writing for translation
- [Non-Translatable Elements](non-translatable-elements.md) — terms that must stay in English
- [Localization Glossary](glossary.md) — translation rules per term
