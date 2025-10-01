# MSSQL Server for RAG สำหรับ Mac/Linux

คู่มือนี้จะแนะนำวิธีการติดตั้งและใช้งาน pyRAGDocs โดยใช้ Conda เป็นตัวจัดการแพ็กเกจและสภาพแวดล้อม

## ข้อกำหนดก่อนเริ่มต้น - ไม่มีไม่ได้ครับ

1. [Conda](https://docs.conda.io/en/latest/miniconda.html) (Miniconda หรือ Anaconda)
2. [Qdrant](https://qdrant.tech/) (vector database สำหรับเก็บ embeddings)
3. [Ollama](https://ollama.ai/) (สำหรับสร้าง embeddings แบบ local) หรือ API key ของ OpenAI

## วิธีการติดตั้ง MSSQL Server for RAG เฉพาะกรณียังไม่เคยติดตั้งมาก่อน

1. **ให้สิทธิ์และรันสคริปต์ติดตั้ง**

   ```bash
  # mac/linux
   chmod +x install_conda.sh
   ./install_conda.sh

   # mac/linux/windows
   conda env create -f environment.yml

  # mac/linux/windows
   conda activate mcp-rag-qdrant-1.1
   pip install ollama

   ollama pull nomic-embed-text
   ```

2. **ตรวจสอบ path ของ python ติดตั้ง**
  [/path/to/conda/bin/python]

   ```bash
   # mac/linux
   which python

   #windows
   where python
   ```

3. **ตั้งค่า Claude Desktop**

   เปิดไฟล์ค่าปรับแต่ง Claude Desktop:
   - macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - Windows: `%APPDATA%\Claude\claude_desktop_config.json`

   เพิ่มการตั้งค่าต่อไปนี้ (แทนที่ `[/path/to/conda/bin/python]` ด้วย path ของ python ติดตั้งไว้แล้ว):

   ```json
   {
     "mcpServers": {
        "mcp-rag-qdrant-1.1": {
        "command": "/path/to/conda/bin/python",
        "args": [
          "/path/to/run.py",
          "--mode",
          "mcp"
        ],
        "env": {
          "QDRANT_URL": "http://34.27.111.38:6333",
          "EMBEDDING_PROVIDER": "ollama",
          "OLLAMA_URL": "http://localhost:11434"
        }
      }
     }
   }
   ```

   ก่อนบันทึกและไปต่อ โปรดทบทวนว่าใช้ local ใน claude_desktop_config.json แล้วถูกต้องใช่หรือไม่ ถ้าไม่ใช่ต้องเปลี่ยน


## ข้อความปฏิเสธความรับผิดชอบ (Disclaimer)

ซอฟต์แวร์ "MSSQL Server for RAG" ("ซอฟต์แวร์") จัดทำขึ้นเพื่อวัตถุประสงค์ทางการศึกษาเท่านั้น ผู้พัฒนาและผู้สอนรวมถึงคณะทำงานที่เกี่ยวข้องไม่รับประกันความถูกต้อง ความสมบูรณ์ หรือความเหมาะสมสำหรับวัตถุประสงค์เฉพาะใดๆ ของซอฟต์แวร์นี้ ไม่ว่าจะโดยชัดแจ้งหรือโดยนัย

การใช้ซอฟต์แวร์นี้เป็นความรับผิดชอบของผู้ใช้แต่เพียงผู้เดียว ผู้พัฒนาและผู้สอนรวมถึงคณะทำงานที่เกี่ยวข้องจะไม่รับผิดชอบต่อความเสียหายใดๆ ทั้งทางตรง ทางอ้อม อุบัติเหตุ พิเศษ หรือเป็นผลสืบเนื่อง รวมถึงแต่ไม่จำกัดเพียงการสูญเสียข้อมูล การสูญเสียกำไร หรือการหยุดชะงักทางธุรกิจ อันเกิดจากการใช้หรือการไม่สามารถใช้ซอฟต์แวร์นี้ได้ แม้ว่าจะได้รับคำแนะนำถึงความเป็นไปได้ของความเสียหายดังกล่าวแล้วก็ตาม

ผู้ใช้รับทราบว่าซอฟต์แวร์นี้อาจมีข้อบกพร่องหรือความผิดพลาด และยอมรับความเสี่ยงทั้งหมดอันเกี่ยวเนื่องกับคุณภาพ ประสิทธิภาพ ความถูกต้อง และการทำงานของซอฟต์แวร์

ผู้ใช้ต้องปฏิบัติตามกฎหมาย ระเบียบ และข้อบังคับที่เกี่ยวข้องทั้งหมดในการใช้ซอฟต์แวร์นี้ รวมถึงแต่ไม่จำกัดเพียงกฎหมายคุ้มครองข้อมูลส่วนบุคคล กฎหมายลิขสิทธิ์ และข้อตกลงการอนุญาตใช้สิทธิใดๆ ที่เกี่ยวข้อง

การใช้ซอฟต์แวร์นี้ถือเป็นการยอมรับข้อกำหนดและเงื่อนไขทั้งหมดที่ระบุไว้ในข้อความปฏิเสธความรับผิดชอบนี้
