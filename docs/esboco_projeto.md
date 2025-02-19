## 📄 Documento de Esboço do Projeto (`/docs/esboco_projeto.md`)

### **Objetivo do projeto** 
Garantir a segurança na comunicação entre funcionários.

### **Tecnologias utilizadas:**
- ✅ **bcrypt** → Hashing seguro de senhas.
- ✅ **PyJWT** → Autenticação via Tokens JWT.
- ✅ **cryptography** → Implementação de AES e RSA.

### **Fluxo básico do sistema:**
1. ✅ **Usuário faz cadastro** (senha armazenada com bcrypt).
2. ✅ **Usuário faz login** (autenticado via JWT).
3. ✅ **Usuário envia uma mensagem criptografada com AES.**
4. ✅ **Apenas o destinatário correto pode descriptografar com sua chave RSA.**
