# apple-silicon-asr-report


I set out to identify the best on-device ASR model for real-time live captioning on macOS by evaluating:

1. **Speed (RTF) vs. Accuracy (EER)**  ![output2 copy](https://github.com/user-attachments/assets/ccb917be-ef6a-432a-a904-dcd2d169bf73)

2. **Language bindings** (Swift vs. Python)  ![output11](https://github.com/user-attachments/assets/4319489b-ffb5-4b85-af4c-3d7f417275b8)

![output](https://github.com/user-attachments/assets/536609ee-9f10-48a0-a95e-6362f9317e02)


---

## Key Takeaways

- **Swift vs. Python performance**  
  - Apple’s built-in Speech framework runs ~30 % faster in Swift than invoked from Python.  
  - `whisper.cpp (tiny.en)` delivers nearly identical RTF in both Swift and Python (≈ 0.012–0.016).

- **Model size matters**  
  - NVIDIA’s Parakeet-TDT-0.6b-v2 boasts excellent RTF but its > 4 GB model file is impractical for distribution.  
  - Whisper.cpp’s tiny models (~ 70 MB) and MLX Whisper (tiny) (~ 40 MB) fit easily—although MLX Whisper currently lacks a native Swift port.

- **Buffer strategy**  
  - Whisper variants excel on long segments (> 30 s), but 100 ms frames introduce timestamp jitter and unstable inference under high call rates.  
  - AppleSpeech handles short buffers gracefully, making it a safer choice when you need consistent sub-100 ms latency.

---

_All code, raw data, and full charts are available in the repo:_  
🔗 https://github.com/wayne-xyz/apple-silicon-asr-report  

