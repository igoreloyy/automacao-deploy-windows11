# 🔧 Automação de Deploy Windows 11 (Sysprep + DISM + Unattend)

## 📌 Visão Geral

Este projeto demonstra a criação de uma imagem customizada do Windows 11 e a automação completa do processo de instalação utilizando:

* Sysprep
* DISM
* Unattend.xml
* Scripts PowerShell

O objetivo é simular um processo de **deploy corporativo**, reduzindo intervenção manual e padronizando estações de trabalho.

---

## 🎯 Objetivos

* Automatizar a instalação do Windows 11
* Padronizar configurações do sistema
* Reduzir tempo de manutenção
* Preparar ambiente para integração com Active Directory

---

## ⚙️ Processo Técnico

### 🔹 1. Preparação do Sistema

* Instalação limpa do Windows 11
* Entrada em Audit Mode assim que ingressar na tela inicial de configuração do Windows 11.

  ```
  Ctrl + Shift + F3
  ```
* Instalação de softwares e configurações
* Limpeza da imagem via CMD:

  ```
  dism /online /cleanup-image /startcomponentcleanup /resetbase
  ```

---

### 🔹 2. Sysprep

Execução do Sysprep.
Ele se encontra em C:\Windows\System32\Sysprep

```
<img width="1919" height="1079" alt="sysprep" src="https://github.com/user-attachments/assets/f00567df-bd06-45ad-9d83-7fb3fa4466d2" />
```

---

### 🔹 3. Captura da Imagem

Captura realizada via DISM.
Realizar boot via pendrive com WindowsRE para manter o disco em estado offline.

```
dism /capture-image /imagefile:D:\install.wim /capturedir:C:\ /name:"Windows-11-Custom"
```

---

### 🔹 4. Criação do Pendrive Bootável

* Criação de mídia bootável via Rufus.
* Substituição do arquivo:

  ```
  <img width="1118" height="626" alt="image" src="https://github.com/user-attachments/assets/c364cbce-2653-4ec5-bd05-781aafd33a83" />

  sources\install.wim
  ```

---

### 🔹 5. Automação com Unattend.xml

* Geração do arquivo `autounattend.xml`
* Inserir XML na pasta raiz do pendrive
* Aplicação automática durante instalação
* Funcionalidades:

  * Criação de usuário local
  * Configuração de timezone
  * Bypass da exigência de internet (NRO)
  * Personalizações conforme necessidade

---

## 🐛 Problemas Encontrados e Soluções

### ❌ Erro 80 no DISM

* **Causa:** uso de parâmetros como `/compress:max`
* **Solução:** captura sem compressão e export posterior

---

### ❌ Sysprep incorreto

* **Causa:** Campo "Generalizar" não marcado
* **Impacto:** imagem inválida para deploy
* **Solução:** execução correta do Sysprep

---

### ❌ autounattend.xml ignorado

* **Causa:** XML incompleto ou inválido
* **Solução:** uso de gerador confiável + estrutura correta

---

### ❌ Exigência de conexão com internet (Windows 11)

* **Causa:** NRO (Network Requirement OOBE)
* **Solução:** bypass via configuração automatizada no autounattend.xml

---

## 🚀 Resultados

* Instalação 100% automatizada
* Redução significativa de tempo
* Padronização do ambiente
* Base pronta para deploy em escala

---

## 🔮 Próximos Passos

* Integração automática com Active Directory
* Renomear computador com padrão (ex: PC-001, PC-002, etc...)
* Deploy via rede
* Implementação de scripts avançados pós-instalação

---

## 🧠 Conclusão

Este projeto demonstra na prática o processo de criação e automação de imagens Windows em um cenário próximo ao ambiente corporativo, incluindo troubleshooting real e resolução de problemas comuns em deploy.

---

## 📎 Autor

Projeto desenvolvido por Igor Eloy Kloch Correa

