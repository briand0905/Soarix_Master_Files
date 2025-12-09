Sure — here’s the **complete .md file** of this full chat (cleaned, formatted, and ready to paste or upload).
It keeps all steps, PowerShell commands, and debugging context for your **Soarix Solutions website fix** — including duplicate component resolution and hero UI upgrade.

Copy the entire block below ⬇️ and save it as:
`soarix-website-debug-notes.md`

---

````markdown
# 🧠 Soarix Solutions — Website Debug & UI Enhancement Log

## 📅 Session Context
**Goal:**  
Make the Soarix Solutions website look as clean and professional as [itsolutions-inc.com](https://www.itsolutions-inc.com), with day/night theme, modern hero section, and correct component structure (no duplicates).

**Tech Stack:**
- React + Vite + TypeScript
- Tailwind CSS
- Fontsource (Poppins, Inter)
- Node.js + npm
- PowerShell for file management

---

## 🐞 Initial Problem
The home page was showing duplicate sections and overlapping content:

- Repeated Navbar and Hero sections.
- Placeholder glow (temporary background layer).
- Fontsource errors (`ENOENT` missing font file path).
- Duplicate `Home.tsx` — one in `src/` and another in `src/pages/`.

---

## ⚙️ Investigation
### 1. Checked for multiple `Home.tsx` files
```powershell
Get-ChildItem -Path .\src\ -Recurse -Filter Home.tsx | Format-Table FullName
````

**Output Example:**

```
C:\Users\RAJ\soarix-solutions\src\Home.tsx
C:\Users\RAJ\soarix-solutions\src\pages\Home.tsx
```

✅ Confirmed two copies exist — both being imported or referenced.

---

## 🔧 Fix Step 1 — Keep only one Home.tsx (under /pages)

We deleted or renamed the duplicate safely to prevent double rendering.

```powershell
# delete extra Home.tsx if exists in src root
if (Test-Path .\src\Home.tsx) { 
  Remove-Item -Force .\src\Home.tsx
  Write-Host "Deleted src\Home.tsx"
} else { 
  Write-Host "No src\Home.tsx found — skip delete"
}
```

---

## 🔧 Fix Step 2 — Ensure App.tsx imports correct page

We updated the import path to use the pages directory.

```powershell
$p = ".\src\App.tsx"
if (Test-Path $p) {
  (Get-Content $p -Raw) -replace "(['""])\.\/Home\1","`$1./pages/Home`$1" | Set-Content $p -Encoding UTF8
  Write-Host "App.tsx updated to import ./pages/Home."
} else {
  Write-Host "App.tsx not found at $p."
}
```

---

## 🧹 Check Step — List remaining Home files and verify imports

```powershell
# confirm file count
Get-ChildItem -Path .\src\ -Recurse -Filter Home*.tsx | Select-Object FullName,LastWriteTime

# check any leftover import
Select-String -Path .\src\**\*.tsx -Pattern "from './Home'" -List | Format-Table Path, LineNumber, Line
```

---

## 🔧 Fix Step 3 — Rebuild Hero Section (Professional Look)

We replaced the existing hero placeholder with a real, glass-style gradient hero section.

```powershell
@'
import React from "react";
import Navbar from "../components/Navbar";

export default function Home(): JSX.Element {
  return (
    <div className="min-h-screen bg-slate-950 text-slate-100 overflow-x-hidden">
      <Navbar />

      {/* Hero Section */}
      <section className="relative isolate overflow-hidden px-6 pt-32 pb-20 sm:pt-40 sm:pb-24 lg:px-8">
        {/* background gradient */}
        <div className="absolute inset-0 -z-10 bg-gradient-to-b from-cyan-950 via-slate-900 to-slate-950 opacity-95"></div>
        {/* blur glow */}
        <div className="absolute inset-x-0 top-[10rem] -z-10 transform-gpu overflow-hidden blur-3xl">
          <div
            className="relative left-[calc(50%-11rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 rotate-[30deg] bg-gradient-to-tr from-sky-500 to-cyan-300 opacity-20 sm:left-[calc(50%-30rem)] sm:w-[72.1875rem]"
          ></div>
        </div>

        {/* hero content */}
        <div className="mx-auto max-w-6xl lg:flex lg:items-center lg:gap-x-12">
          {/* text */}
          <div className="max-w-2xl">
            <h1 className="text-4xl font-bold tracking-tight sm:text-6xl leading-snug">
              Transforming Ideas into{" "}
              <span className="bg-gradient-to-r from-sky-400 via-cyan-300 to-emerald-300 text-transparent bg-clip-text">
                Intelligent Digital Realities
              </span>
            </h1>
            <p className="mt-6 text-lg leading-8 text-slate-300">
              From 3D visualization to intelligent automation — Soarix Solutions
              blends creativity, psychology, and AI to build emotionally
              intelligent digital systems.
            </p>
            <div className="mt-10 flex flex-wrap gap-4">
              <a
                href="/solutions"
                className="px-6 py-3 rounded-xl bg-gradient-to-r from-sky-500 to-cyan-400 text-slate-900 font-semibold shadow-md hover:scale-[1.02] transition-transform"
              >
                Explore Our Solutions
              </a>
              <a
                href="/contact"
                className="px-6 py-3 rounded-xl border border-slate-700 text-slate-200 hover:border-slate-500"
              >
                Book Free Consultation
              </a>
            </div>
          </div>

          {/* glass card */}
          <div className="mt-12 flex justify-center lg:mt-0 lg:flex-shrink-0">
            <div className="relative w-[320px] h-[320px] rounded-3xl bg-gradient-to-br from-sky-400/10 to-cyan-200/10 border border-sky-400/20 shadow-[0_0_50px_-15px_rgba(0,200,255,0.3)] backdrop-blur-xl flex items-center justify-center text-center">
              <p className="text-lg font-semibold text-sky-300">
                Future of AI Design <br /> starts with Soarix
              </p>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="border-t border-slate-800 mt-12">
        <div className="max-w-6xl mx-auto px-6 py-8 text-center text-slate-500 text-sm">
          © {new Date().getFullYear()} Soarix Solutions — All rights reserved.
        </div>
      </footer>
    </div>
  );
}
'@ | Set-Content -Path .\src\pages\Home.tsx -Encoding UTF8
```

---

## 🚀 Run and Refresh

```powershell
npm run dev
```

Then **Ctrl + Shift + R** in browser to hard refresh.

Expected Output:

* Single Navbar
* One centered Hero Section
* Gradient + glow background
* Two buttons (primary + outline)
* Subtle glass card effect

---

## ✅ Next Steps (Pending)

Once duplicate issue fully resolved:

1. Add scroll-trigger animations (Framer Motion).
2. Create 5 Branches cards grid.
3. Include parallax glow or floating lines animation.
4. Finish footer links + social icons.
5. Add Day/Night theme toggle synced with system preference.

---

## 💡 Learning Notes

* Always verify import paths in Vite projects.
* Keep only one page per route.
* Use Tailwind for design control; gradients and glow are cheaper than images.
* Fontsource paths can cause ENOENT if you import wrong weight/style variants.

---

### 🧩 Author

**Orchestrated by:**
AI CTO for Soarix Solutions
**Session Partner:** Brian (Founder)

**Objective:**
Turn ideas into scalable, emotionally intelligent systems with ethical AI foundations.

---

```

---

Would you like me to extend this `.md` file with the **next stage** (animations, cards, and footer polish) so it’s fully production-ready?
```
