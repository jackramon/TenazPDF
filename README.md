# TenazPDF

**30 ferramentas de PDF no seu computador — sem nuvem, sem cadastro, sem limite de uso.**

[![Versão](https://img.shields.io/github/v/release/jackramon/TenazPDF)](https://github.com/jackramon/TenazPDF/releases) ![Licença](https://img.shields.io/badge/licen%C3%A7a-todos%20os%20direitos%20reservados-lightgrey)

## O que é

Um aplicativo de desktop (Windows) com **30 ferramentas de PDF 100% locais**: todo processamento acontece dentro da sua máquina — nenhum arquivo sai dela. Sem cadastro, sem cota, sem marca d'água forçada, sem esperar na fila de nenhum serviço online. O app é um shell Electron com um backend FastAPI local (127.0.0.1) e interface React; os dados ficam em `%LOCALAPPDATA%\TenazPDF` e o fechamento da janela encerra tudo.

### As 30 ferramentas

| Grupo | Ferramenta | O que faz |
|---|---|---|
| **Organizar** | Juntar PDF | Une dois ou mais PDFs, com arrastar-ordenar |
| | Dividir PDF | Intervalos ("1-3, 7, 9-12"), extrair páginas ou dividir em partes — resultado em ZIP |
| | Organizar PDF | Reordenar, remover, duplicar páginas e inserir de um 2º PDF, com miniaturas reais |
| | Rodar PDF | 90°/180°/270° em todas ou nas páginas escolhidas (rotação acumulativa) |
| | Recortar PDF | Arraste a área a manter ou remova margens (oculta, não remove) |
| **Converter** | PDF → Imagem | Páginas em JPG/PNG de 72 a 300 dpi |
| | Imagem → PDF | Até 20 JPG/PNG em A4 ou no tamanho exato da imagem |
| | Word → PDF | Cascata de motores: Office instalado → LibreOffice → conversão simplificada |
| | Excel → PDF | Mesma cascata, com as tabelas reais da planilha |
| | PowerPoint → PDF | Idem, com os slides fielmente renderizados |
| | HTML → PDF | HTML colado impresso com a fidelidade do Chrome (Chromium embutido no app) |
| | URL → PDF | Página da web pública → PDF, com preview, viewport e opções de página |
| | PDF → Word | Texto editável (reflow com o próprio Word quando disponível) |
| | PDF → Excel | Tabelas detectadas e extraídas por página |
| | PDF → PowerPoint | 1 slide por página, com a aparência visual |
| | PDF → Markdown | Texto estrutural (títulos, listas, tabelas; imagens em ZIP opcional) |
| | PDF → PDF/A | PDF/A-2b para arquivamento de longo prazo |
| | OCR | Texto reconhecido em escaneados (por/eng/spa **embutidos**) → PDF pesquisável |
| **Editar** | Editar PDF | Anotações visuais: texto, formas, setas, desenho, carimbos, marcações |
| | Editar texto | Substituição cirúrgica de trechos, ou round-trip via Word |
| | Marca d'água | Texto ou imagem, opacidade, rotação e 9 posições, com preview ao vivo |
| | Numeração de páginas | Formatos personalizáveis (`{page}`/`{total}`), posição e cor |
| | Preencher formulários | Campos AcroForm existentes (texto, checkbox, rádio, lista) com achatar opcional |
| **Segurança** | Proteger PDF | Senha AES-256 + permissões (imprimir/copiar/modificar) |
| | Desbloquear PDF | Remove a senha de arquivos que você já abre |
| | Ocultar informação | Redação REAL: tarjas manuais ou por busca — o conteúdo deixa de existir |
| | Assinar PDF | Assinatura visual: digitada (fontes manuscritas) ou imagem, posicionada com clique |
| | Comparar PDF | Diferenças de texto, aparência e estrutura entre dois documentos |
| | Reparar PDF | Recupera corrompidos/truncados por cascata de motores, com oráculos estritos |
| **Fluxos** | Comprimir PDF | Re-sampling nativo em 3 níveis (150/100/72 dpi) |

O grupo **Fluxos** também inclui o encadeamento **"Continuar para..."**: concluída qualquer ferramenta que produz um PDF único, a tela de resultado oferece as próximas etapas naturais (juntou → comprimir, numerar, proteger) já com o arquivo carregado, sem re-upload — e o nome de saída preserva sempre o nome base do arquivo original.

## Instalar

1. Na página de [Releases](https://github.com/jackramon/TenazPDF/releases), baixe **`TenazPDF Setup X.Y.Z.exe`** (instalador — escolhe a pasta, cria atalho) ou **`TenazPDF X.Y.Z.exe`** (portable — roda sem instalar).
2. Duplo clique e pronto: sem navegador, nada a instalar além do próprio app.
3. O atalho **TenazPDF** abre a janela; fechar a janela encerra o app inteiro.

> ⚠️ **SmartScreen**: o binário não é assinado digitalmente (certificado de assinatura de código é pago). Na primeira execução o Windows pode mostrar "O Windows protegeu o seu computador". Passo a passo: clique em **"Mais informações"** → **"Executar assim mesmo"**. Se o antivírus apontar o portable, é falso positivo esperado do empacotador — o instalador `Setup` é a via mais limpa.

## Como atualizar

**Pelo app (caminho normal)**: na página **Sobre** (botão ℹ️ do cabeçalho), clique em **Checar atualizações**. Com versão nova disponível, aparece o botão **Baixar e instalar**: o app baixa o instalador, confere automaticamente o SHA256 dele contra o checksum publicado na release e só então executa a instalação — arquivo que não passar na verificação nunca é executado.

**Manualmente**: na página de [Releases](https://github.com/jackramon/TenazPDF/releases), baixe o `TenazPDF Setup X.Y.Z.exe` da versão desejada (ou o portable `TenazPDF X.Y.Z.exe`). Para conferir a integridade antes de executar, baixe também o `TenazPDF-X.Y.Z-SHA256.txt` da mesma release e compare no PowerShell:

```
Get-FileHash .\TenazPDF.Setup.X.Y.Z.exe -Algorithm SHA256
```

O hash exibido precisa ser igual ao da linha correspondente do `.txt` (a linha do `Setup` para o instalador; maiúsculas e minúsculas não importam na comparação).

## Privacidade

**Telemetria zero**: o app não coleta dados, não envia estatísticas e não faz chamadas externas no boot — sem analytics, sem "phone home". As únicas saídas de rede possíveis são as 3 exceções declaradas:

1. **URLs que você converter** em HTML/URL → PDF, carregadas pelo navegador embutido do próprio app;
2. **checagem de atualizações**, só quando você clica em "Checar atualizações" na página Sobre;
3. **APIs de IA que você configurar** com a sua própria chave — o app nunca as chama por conta própria.

A declaração também está dentro do app (página *Sobre*), com a versão instalada e os créditos técnicos.

## Manual e FAQ

O manual completo vive **dentro do app**: botão 📖 no cabeçalho (ou **ℹ️** para a página Sobre). Resumo do FAQ:

- **O app abre uma vez só?** Sim — lock de instância única; um fechamento forçado que deixe locks órfãos em `%LOCALAPPDATA%\TenazPDF` é detectado e limpo sozinho no próximo boot.
- **Antivírus reclamou do executável?** Falso positivo esperado (binário não assinado); prefira o instalador `Setup`.
- **Nomes de saída em português?** Sim: `documento_unido.pdf`, `documento_comprimido.pdf`, `documento_assinado.pdf`… — e nas cadeias o nome base original sempre preservado, sem sufixos acumulando.
- **PDF/A invalida assinatura?** Sim, é verdade criptográfica (a assinatura cobre os bytes exatos; qualquer reescrita invalida a verificação). O app avisa e nunca bloqueia; o original assinado permanece intacto no disco.

## Limitações conhecidas

- **SmartScreen** em binário não assinado (ver passo a passo em Instalar).
- **Office → PDF sem Office/LibreOffice na máquina**: cai na conversão *simplificada* declarada (fallback puro-Python) — fidelidade perfeita exige um motor real instalado; o app mostra o motor usado no resultado.
- **Comparar PDF pausado**: o polimento ficou abaixo de ferramentas semelhantes disponíveis online e a ferramenta foi pausada por decisão do dono — as 3 dimensões funcionam, mas o refinamento está pendente.
- A conversão **PDF → Markdown** é estrutural (títulos, listas, tabelas) — o layout visual não é preservado.

## Licença

Projeto pessoal — **todos os direitos reservados**. Uso e distribuição por terceiros dependem de autorização do autor. (Uma licença open source, ex. MIT, pode ser adicionada depois por decisão do dono.)
