
# TcpNsiKill

> 🔍 Uma ferramenta orientada à pesquisa para o encerramento de conexões TCP de baixo nível no Windows usando interfaces NSI não documentadas.
> 🧪 Apenas para fins de testes de segurança, simulações de red team e fins educacionais.

---
Blog: [https://kyxiaxiang.github.io/2025/06/06/%E6%B5%85%E6%B5%85%E5%88%86%E6%9E%90%E9%93%B6%E7%8B%90%E6%9C%80%E6%96%B0%E6%96%AD%E7%BD%91%E6%89%8B%E6%B3%95/](https://kyxiaxiang.github.io/2025/06/06/%E6%B5%85%E6%B5%85%E5%88%86%E6%9E%90%E9%93%B6%E7%8B%90%E6%9C%80%E6%96%B0%E6%96%AD%E7%BD%91%E6%89%8B%E6%B3%95/)
---

## ✨ O que é isto?

**TcpNsiKill** fornece um método furtivo em modo de usuário (user-mode) para encerrar conexões TCP de processos específicos, contornando o `SetTcpEntry()` e hooks em nível de API.

Ele se comunica diretamente com o driver de dispositivo `\\.\Nsi` usando funções nativas do NT, como `NtDeviceIoControlFile`.

---

## 🎯 Caso de Uso

- ✅ Simular a desconexão por processo em ambientes de red team
- ✅ Pesquisar como softwares de segurança dependem da conectividade de rede
- ✅ Desenvolver mecanismos de controle TCP indetectáveis para estudo

---

## ⚙️ Como Funciona

1. Enumera todas as conexões TCP ativas através de `GetTcpTable2`
2. Identifica o processo alvo pelo nome ou PID
3. Constrói um payload de 72 bytes (`NSI_SET_PARAMETERS_EX`)
4. Envia um IOCTL (0x120013) para `\\.\Nsi` através de `NtDeviceIoControlFile`

---

## 🧱 Estrutura do Projeto

| Arquivo | Propósito |
|---|---|
| `TcpNsiKill.cpp` | Lógica principal do código |
| `README.md` | Descrição do projeto |

---

## 🚀 Uso Rápido

1. Compile com o Visual Studio (recomendado: x64, modo Release)
2. Execute como administrador
3. Modifique a lista de processos alvo em `targetProcs` no código
4. Observe as conexões sendo forçadamente encerradas

> ⚠️ Funciona apenas no Windows onde o driver NSI está disponível (nativo do Windows)

---

## 🧠 Referências

- Microsoft Docs - [GetTcpTable2](https://learn.microsoft.com/en-us/windows/win32/api/iphlpapi/nf-iphlpapi-gettcptable2)
- Análise reversa da implementação de `SetTcpEntry`
- Inspirado por: [post de x86matthew](https://www.x86matthew.com/view_post?id=settcpentry6)

---

## 🧭 Uso Legal

**Este projeto é estritamente para fins educacionais, pesquisa ética e simulação em ambientes autorizados.**

> ❌ NUNCA use em sistemas não autorizados
> ✅ SEMPRE siga as leis locais e as políticas de segurança

---
Conta pública do WeChat: 41group
Original: [https://www.notion.so/209c6252b11b802fa69bdde1c05ac01b?source=copy_link](https://www.notion.so/209c6252b11b802fa69bdde1c05ac01b?source=copy_link)
