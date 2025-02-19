## 📄 Proposta de Implementação 

### **Explicação de como cada tecnologia será usada no sistema.**

Este projeto tem como objetivo garantir que as mensagens trocadas entre os usuários sejam seguras, ou seja, que ninguém além do remetente e do destinatário possa ler o conteúdo. Para isso, usamos algumas tecnologias conhecidas por sua eficiência em segurança da informação:

- **bcrypt:** O bcrypt transforma essa senha em um "código embaralhado" (hash). Assim, mesmo que alguém invada o banco de dados, não verá a senha real, só o hash dela.  

- **PyJWT:** JWT (JSON Web Token) é como um “passe de entrada” para o sistema. Quando você faz login, o sistema te dá um token que confirma que você está autenticado. Esse token é usado para acessar as funcionalidades sem precisar fazer login toda hora.  

- **Cryptography (AES e RSA):**
  - **AES:** É como se fosse um cadeado para proteger as mensagens. Cada mensagem tem seu próprio cadeado (chave AES), garantindo que mesmo que alguém intercepte a conversa, não consiga entender nada.  
  - **RSA:** É um sistema de duas chaves: uma pública (para trancar) e uma privada (para destrancar). Usamos o RSA para proteger as chaves AES. Assim, só o destinatário certo consegue abrir a mensagem.  

---

### **Principais etapas de implementação, incluindo:**

1. ✅ **Cadastro de usuário → Hash de senha com bcrypt.**  
   - Quando você se cadastra, sua senha não é salva como "123456", mas como um código gerado pelo bcrypt. Mesmo que alguém acesse o banco de dados, não verá a senha original.  

2. ✅ **Login → Geração e verificação de Token JWT.**  
   - Ao fazer login, o sistema verifica sua senha. Se estiver correta, gera um token JWT que serve como seu "passe de acesso". Com ele, você pode navegar pelo sistema sem digitar a senha de novo.  

3. ✅ **Criptografia de mensagens → Uso de AES (CBC).**  
   - Quando você envia uma mensagem, ela é criptografada com AES no modo CBC (um jeito mais seguro de embaralhar os dados). Mesmo que alguém intercepte, só verá um monte de caracteres sem sentido.  

4. ✅ **Proteção da chave AES → Uso de RSA para criptografar a chave antes de armazená-la.**  
   - A chave usada para criptografar a mensagem (AES) também é protegida. Ela é trancada com a chave pública RSA do destinatário. Só ele, com sua chave privada, poderá destrancar e ler a mensagem.  

---

### **Breve explicação sobre armazenamento seguro de dados.**

O sistema cuida bem dos dados em todas as etapas:

- **Senhas:** Só são armazenadas como hash, nunca em texto simples.  
- **Mensagens:** Ficam criptografadas com AES no banco de dados. Mesmo que o banco seja invadido, as mensagens continuam protegidas.  
- **Chaves AES:** Cada chave AES usada para criptografar uma mensagem é armazenada de forma segura, trancada com a chave pública RSA do destinatário.  
- **Tokens JWT:** Servem para autenticação e têm prazo de validade. Quando expiram, o usuário precisa fazer login novamente.  
