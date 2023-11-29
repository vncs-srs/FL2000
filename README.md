# Driver de kernel Fresco Logic FL2000 Linux/Android

### 1. O que é isso?

Este é um lançamento oficial de driver da Fresco Logic em uma tentativa de ajudar a comunidade de código aberto a adotar o desenvolvimento e uso do dispositivo FL2000DX.
Este driver cobre apenas a parte USB da lógica de exibição. Ele não oferece suporte à lógica de desktop Linux (por exemplo, desktop estendido versus desktop espelhado).

### 2. Em quais versões do kernel esse driver funciona?

Este driver foi testado no Ubuntu 14 LTS, bem como em algumas plataformas Android com kernel versão 3.10.x.
Esta fonte de driver pode não ser compilada em kernels mais recentes (por exemplo, 4.0 ou superior) devido às mudanças rápidas da API no
kernel principal. Talvez seja necessário adaptá-lo para seu próprio uso.

### 3. Público-alvo

Esta versão é direcionada a desenvolvedores de código aberto, e não a usuários finais.

### 4. Como habilito a área de trabalho estendida/área de trabalho espelhada em meu X Window?

Atualmente o Fresco Logic não fornece manipulação relacionada à área de trabalho.
A Fresco Logic espera que a comunidade contribua nesta área para que os usuários finais possam adotar facilmente esta solução.

### 5. Limitação do FL2000DX.

O chip FL2000DX é barato por design, onde não possui um buffer de quadros próprio.
Ele depende muito da velocidade de transferência do USB 3.0 para acomodar o fluxo USB contínuo.
Quanto maior for a imagem, mais pesada ela depende da largura de banda USB.
Um típico 1920x1080@60 Hz requer 1920 * 1080 * 24bpp * 60 = 373.248.000 bytes/s de tráfego no barramento USB.
Como tal, a velocidade USB2.0 não é suportada.

A conexão de mais de um dispositivo FL2000DX ao mesmo barramento está obsoleta.

### 6. Como compilar e testar o driver do kernel?
#### 6a. Compilar o driver

Encontre a árvore fonte do seu kernel e edite `src/Makefile`. Localize a seguinte linha:
    
    KERNEL_PATH = /usr/src/linux-headers-4.4.0-72-generic`
    
Modifique esta linha para que aponte para a árvore de origem correta.
Depois disso, execute `make` para criar `fl2000.ko` e execute `insmod fl2000.ko` para carregar o driver.

####6b. Teste o driver

Na pasta `sample`, execute `make` para criar `fltest`. Se você estiver usando um
compilador cruzado para construir o binário para plataformas específicas, você precisa especificar esse específico
compilador em `src/Makefile`.
    
Execute `./fltest 0` como superusuário para executar o teste. O driver fornece vários
métodos de acesso ao buffer no modo de usuário (por exemplo, copiar para o buffer interno do kernel ou
bloqueando diretamente o buffer do usuário). Veja `fl2000_ioctl.h` para detalhes
Informação.

### 7. Como faço para registrar um bug para os desenvolvedores do Fresco Logic?

Você pode registrar bugs em [Github Issues](https://github.com/fresco-fl2000/fl2000/issues)



