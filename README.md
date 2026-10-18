
# vedioforge-ai

"use client";

import { useState } from "react";

export default function Home() {
  const [mode, setMode] = useState("Text to Video");
  const [prompt, setPrompt] = useState("");
  const [image, setImage] = useState<File | null>(null);
  const [message, setMessage] = useState("");
  const [credits, setCredits] = useState(50);

  function generate() {
    if (!prompt.trim()) {
      setMessage("Please enter your video description.");
      return;
    }

    if (mode === "Image to Video" && !image) {
      setMessage("Please upload an image first.");
      return;
    }

    if (credits < 10) {
      setMessage("Not enough demo credits.");
      return;
    }

    setCredits((current) => current - 10);
    setMessage(
      "Request validated! Connect an AI video API to generate your actual video."
    );
  }

  return (
    <main className="min-h-screen bg-[#090909] text-white">
      <header className="flex items-center justify-between border-b border-[#333] p-5">
        <h1 className="text-xl font-black text-[#d4af37]">
          ✦ VideoForge AI
        </h1>
        <span className="text-sm text-[#d4af37]">
          Credits: {credits}
        </span>
      </header>

      <section className="mx-auto max-w-3xl px-5 py-12">
        <p className="mb-3 text-sm uppercase tracking-[.25em] text-[#d4af37]">
          Your imagination, powered by AI
        </p>

        <h2 className="mb-4 text-4xl font-black sm:text-6xl">
          Create videos.
          <br />
          <span className="text-[#d4af37]">Bring ideas to life.</span>
        </h2>

        <p className="mb-8 text-gray-400">
          Create cinematic content from text or images.
          Built for creators everywhere.
        </p>

        <div className="rounded-2xl border border-[#383328] bg-[#141414] p-5">
          <div className="mb-5 grid grid-cols-2 gap-3">
            {["Text to Video", "Image to Video"].map((item) => (
              <button
                key={item}
                onClick={() => {
                  setMode(item);
                  setMessage("");
                }}
                className={`rounded-xl border p-3 ${
                  mode === item
                    ? "border-[#d4af37] bg-[#302713] text-[#f4d778]"
                    : "border-[#383838] text-gray-300"
                }`}
              >
                {item}
              </button>
            ))}
          </div>

          <label className="mb-2 block font-semibold">
            Describe your video
          </label>

          <textarea
            value={prompt}
            onChange={(e) => setPrompt(e.target.value)}
            placeholder="A beautiful cinematic Hausa village at sunset..."
            className="mb-4 min-h-32 w-full rounded-xl border border-[#383838] bg-[#090909] p-4 outline-none focus:border-[#d4af37]"
          />

          {mode === "Image to Video" && (
            <label className="mb-4 block cursor-pointer rounded-xl border border-dashed border-[#d4af37] p-5 text-center text-gray-300">
              {image ? image.name : "Upload an image"}
              <input
                type="file"
                accept="image/png,image/jpeg,image/webp"
                className="mt-3 block w-full text-sm"
                onChange={(e) =>
                  setImage(e.target.files?.[0] ?? null)
                }
              />
            </label>
          )}

          <label className="mb-2 block font-semibold">
            Video format
          </label>

          <select className="mb-5 w-full rounded-xl border border-[#383838] bg-[#090909] p-3">
            <option>16:9 — YouTube</option>
            <option>9:16 — Shorts and TikTok</option>
            <option>1:1 — Square video</option>
          </select>

          <button
            onClick={generate}
            className="w-full rounded-xl bg-[#d4af37] p-4 font-bold text-black hover:bg-[#f0d36e]"
          >
            ✨ Create AI Video — 10 Credits
          </button>

          {message && (
            <p className="mt-4 rounded-lg bg-[#242016] p-4 text-sm text-[#f4d778]">
              {message}
            </p>
          )}
        </div>

        <div className="mt-8 grid grid-cols-2 gap-3 sm:grid-cols-4">
          {[
            "Hausa Voice",
            "Subtitles",
            "Video Downloads",
            "Admin Dashboard",
          ].map((feature) => (
            <div
              key={feature}
              className="rounded-xl border border-[#333] p-4 text-center text-sm text-gray-300"
            >
              {feature}
            </div>
          ))}
        </div>

        <p className="mt-8 text-center text-xs text-gray-500">
          VideoForge AI · Free-tier development starter
        </p>
      </section>
    </main>
  );
}
