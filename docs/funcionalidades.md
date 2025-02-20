## O que o sistema faz?

O sistema foi pensado para garantir que as mensagens trocadas entre os usuários sejam privadas e seguras. Aqui está o passo a passo do que acontece:  

### **Cadastro de usuário → Protege a senha com bcrypt antes de armazenar.**  
Quando você se cadastra, o sistema não salva sua senha diretamente. Em vez disso, ela passa por um processo chamado *hashing* com bcrypt. É como transformar a senha em um código embaralhado. Assim, mesmo que alguém acesse o banco de dados, só verá esse código, não a senha original.  

### **Login → Se a senha estiver correta, gera um Token JWT.**  
Ao fazer login, o sistema compara a senha digitada com o hash armazenado. Se estiver tudo certo, ele gera um *Token JWT*, que funciona como um "passe de entrada". Com esse token, você pode acessar o sistema sem precisar ficar digitando sua senha a cada clique.  

### **Enviar mensagem → A mensagem é criptografada com AES antes de ser salva.**  
Quando você envia uma mensagem, ela é trancada com uma chave especial usando o algoritmo AES. Imagine colocar a mensagem em um cofre e fechar com um cadeado. Mesmo que alguém acesse o banco de dados, só verá um monte de caracteres embaralhados, sem sentido.  

### **Receber mensagem → O usuário descriptografa com RSA sua chave AES e acessa a mensagem.**  
Para abrir a mensagem, o destinatário precisa da chave que tranca o cofre (a chave AES). Mas essa chave também está protegida! Ela foi trancada com a chave pública RSA do destinatário. Só ele, com sua chave privada, consegue destrancar e ler a mensagem
