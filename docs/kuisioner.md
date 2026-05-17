## Problem Statement
Jelaskan permasalahan utama yang ingin Anda selesaikan. Sertakan konteks, siapa yang terdampak, dan mengapa masalah ini penting untuk diselesaikan.

## Target Users
Jelaskan siapa pengguna utama dari solusi Anda. Sebutkan karakteristik, kebutuhan, dan konteks penggunaan mereka.

## Potential Impact 
Jelaskan bagaimana solusi berbasis AI yang Anda buat dapat menyelesaikan permasalahan yang diangkat, serta manfaat yang dihasilkan bagi pengguna atau stakeholder.
Jika ya, jelaskan improvisasi atau modifikasi yang kamu lakukan terhadap project mu
answer:
- LLM Provider -> change to OpenRouter with Xiaomi models, from the original Google Gemini.
- Change context, adjust System Prompt, to compensate with Analyzing Insurance Policy
- Change flow, adjust LLM2 to with Agent-mode to allow followup question
- Add Chat Input for start trigger, rather than the original run flow trigger button
- Use git repository to track changes.

## Penjelasan singkat alur sistem (input → proses → output) yang digunakan

## Potensi Pengembangan Lanjutan dari project mu (Pengisian Optional)
penjelasan tentang ide atau rencana pengembangan ke depan dari project yang kamu buat.
Isi bagian ini dengan kemungkinan fitur tambahan, peningkatan sistem, atau perluasan penggunaan project agar lebih bermanfaat dan relevan di masa depan.

## Apakah setelah mengembangkan capstone project Anda, muncul potensi ide project lain yang bisa di buat? Jika iya jelaskan (Pengisian Optional)
Bagian ini diisi dengan contoh judul ide project baru yang muncul setelah kamu mengembangkan capstone project. Judul yang dituliskan sebaiknya menggambarkan solusi atau use case lain yang masih relevan atau merupakan pengembangan dari project utamamu, misalnya di bidang HR, automation, atau AI assistant.

Answer:
- I want to create an MCP (Model Context Protocol) library that has all peraturan (ranged from UUs, Perpres, Permen, Perda, Pergub) so that the other LLM agent can consume it, it will reduce hallucination by a lot, large difference, because the model now have a valid logical ground. current peraturan.go.id is only provide pdf format, with no query features, kust a pile of pdf peraturan legal documents.