<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Configurador Moderno de Certificados</title>
    <style>
        :root {
            --bg-principal: #f8fafc;
            --bg-card: #ffffff;
            --border-cor: #e2e8f0;
            --cor-primaria: #3b82f6;
            --cor-primaria-hover: #eff6ff;
            --texto-principal: #1e293b;
            --texto-secundario: #64748b;
        }

        body {
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
            background-color: var(--bg-principal);
            color: var(--texto-principal);
            padding: 40px 20px;
            margin: 0;
        }

        h2 {
            font-weight: 700;
            margin-bottom: 24px;
            color: #0f172a;
        }

        /* Container que força o fluxo horizontal moderno */
        .fluxo-horizontal {
            display: flex;
            flex-direction: row;
            align-items: stretch;
            gap: 24px;
            overflow-x: auto;
            padding: 12px 4px;
            scroll-behavior: smooth;
            
            background: 1px #244595;
            border-radius: 15px;
            padding: 20px;
        }

        /* Coluna que agrupa as opções de cada passo */
        .coluna-passo {
            display: flex;
            flex-direction: column;
            gap: 12px;
            min-width: 260px;
            max-width: 320px;
            animation: fadeIn 0.3s ease-out forwards;
        }

        .titulo-passo {
            font-size: 13px;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            color: var(--texto-secundario);
            font-weight: 600;
            margin-bottom: 4px;
        }

        /* Grid para os botões/cards dentro de cada passo */
        .grid-opcoes {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        /* O Card interativo que substitui o Select */
        .card-opcao {
            background-color: var(--bg-card);
            border: 2px solid var(--border-cor);
            border-radius: 12px;
            padding: 16px;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            flex-direction: column;
            gap: 4px;
            user-select: none;
        }

        .card-opcao:hover {
            border-color: var(--cor-primaria);
            background-color: var(--cor-primaria-hover);
            transform: translateY(-1px);
        }

        /* Estado ativo/selecionado */
        .card-opcao.selecionado {
            border-color: var(--cor-primaria);
            background-color: var(--cor-primaria-hover);
            box-shadow: 0 4px 12px rgba(59, 130, 246, 0.15);
        }

        .opcao-titulo {
            font-weight: 600;
            font-size: 15px;
        }

        .opcao-subtitulo {
            font-size: 13px;
            color: var(--texto-secundario);
        }

        .preco-destaque {
            font-size: 16px;
            font-weight: 700;
            color: var(--cor-primaria);
            margin-top: 6px;
        }

        /* Classe utilitária para esconder os passos futuros */
        .hidden {
            display: none !important;
        }

        /* Animação suave para o surgimento das colunas ao lado */
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateX(15px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        /* Customização da barra de rolagem horizontal */
        .fluxo-horizontal::-webkit-scrollbar {
            height: 8px;
        }
        .fluxo-horizontal::-webkit-scrollbar-track {
            background: #f1f5f9;
            border-radius: 4px;
        }
        .fluxo-horizontal::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        
        .nuvem{
            display: flex;
            flex-direction: row;
        }
        
        .coluna-passo-nuvem{
            width: 420px;
        }
    </style>
</head>
<body>

    <h2>Emitir Certificado Digital</h2>
    
    <div class="fluxo-horizontal" id="fluxoConteiner">
        
        <div class="coluna-passo" id="passo-1">
            <div class="titulo-passo">1. Identificação</div>
            <div class="grid-opcoes">
                <div class="card-opcao" onclick="selecionarOpcao(1, 'tipo', 'cpf', this)">
                    <div class="opcao-titulo">Pessoa Física</div>
                    <div class="opcao-subtitulo">Quero usar CPF</div>
                </div>
                <div class="card-opcao" onclick="selecionarOpcao(1, 'tipo', 'cnpj', this)">
                    <div class="opcao-titulo">Pessoa Jurídica</div>
                    <div class="opcao-subtitulo">Quero usar CNPJ</div>
                </div>
            </div>
        </div>

        <div class="coluna-passo hidden" id="passo-2">
            <div class="titulo-passo">2. Tipo de Certificado</div>
            <div class="grid-opcoes">
                <div class="card-opcao" onclick="selecionarOpcao(2, 'modelo', 'a1', this)">
                    <div class="opcao-titulo">Certificado A1</div>
                    <div class="opcao-subtitulo">Instalado direto no computador</div>
                </div>
                <div class="card-opcao" onclick="selecionarOpcao(2, 'modelo', 'a3', this)">
                    <div class="opcao-titulo">Certificado A3</div>
                    <div class="opcao-subtitulo">Uso em mídias físicas ou token</div>
                </div>
                <div class="card-opcao" onclick="selecionarOpcao(2, 'modelo', 'nuvem', this)">
                    <div class="opcao-titulo">Certificado Nuvem</div>
                    <div class="opcao-subtitulo">Nuves - Seguro e multiplataforma</div>
                </div>
            </div>
        </div>

        <div class="coluna-passo hidden" id="passo-3-a1">
            <div class="titulo-passo">3. Validade & Preço</div>
            <div class="grid-opcoes">
                <div class="card-opcao selecionado">
                    <div class="opcao-titulo">Arquivo Digital</div>
                    <div class="opcao-subtitulo">Validade de 12 meses</div>
                    <div class="preco-destaque">R$ 149,00</div>
                </div>
            </div>
        </div>

        <div class="coluna-passo hidden" id="passo-3-a3">
            <div class="titulo-passo">3. Escolha a Mídia</div>
            <div class="grid-opcoes">
                <div class="card-opcao" onclick="selecionarOpcao(3, 'midia', 'token', this)">
                    <div class="opcao-titulo">Token USB</div>
                    <div class="opcao-subtitulo">Dispositivo móvel homologado</div>
                </div>
                <div class="card-opcao" onclick="selecionarOpcao(3, 'midia', 'cartao', this)">
                    <div class="opcao-titulo">Cartão Inteligente</div>
                    <div class="opcao-subtitulo">Necessita de leitora</div>
                </div>
                <div class="card-opcao" onclick="selecionarOpcao(3, 'midia', 'renovacao', this)">
                    <div class="opcao-titulo">Renovação</div>
                    <div class="opcao-subtitulo">Usar mídia que já possuo</div>
                </div>
            </div>
        </div>

        <div class="coluna-passo hidden" id="passo-4-a3">
            <div class="titulo-passo">4. Validade & Preço</div>
            <div class="grid-opcoes">
                <div class="card-opcao" onclick="selecionarOpcao(4, 'validadeA3', '12', this)">
                    <div class="opcao-titulo">Plano 12 Meses</div>
                    <div class="opcao-subtitulo">Uso por 1 ano</div>
                    <div class="preco-destaque">R$ 280,00</div>
                </div>
                <div class="card-opcao" onclick="selecionarOpcao(4, 'validadeA3', '24', this)">
                    <div class="opcao-titulo">Plano 24 Meses</div>
                    <div class="opcao-subtitulo">Melhor custo-benefício</div>
                    <div class="preco-destaque">R$ 420,00</div>
                </div>
            </div>
        </div>

        <div class="coluna-passo-nuvem hidden" id="passo-3-nuvem">
            <div class="titulo-passo">3. Período Nuves</div>
            <div class="grid-opcoes nuvem">
                <div>
                    <div class="card-opcao" onclick="selecionarOpcao(3, 'validadeNuvem', '3', this)">
                        <div class="opcao-titulo">A3 Nuves 3 meses</div>
                        <div class="opcao-subtitulo">Acesso trimestral</div>
                        <div class="preco-destaque">R$ 79,00</div>
                    </div>
                    <div class="card-opcao" onclick="selecionarOpcao(3, 'validadeNuvem', '6', this)">
                        <div class="opcao-titulo">A3 Nuves 6 meses</div>
                        <div class="opcao-subtitulo">Acesso semestral</div>
                        <div class="preco-destaque">R$ 129,00</div>
                    </div>
                </div>
                <div>
                    <div class="card-opcao" onclick="selecionarOpcao(3, 'validadeNuvem', '12', this)">
                        <div class="opcao-titulo">A3 Nuves 12 meses</div>
                        <div class="opcao-subtitulo">Acesso anual</div>
                        <div class="preco-destaque">R$ 219,00</div>
                    </div>
                    <div class="card-opcao" onclick="selecionarOpcao(3, 'validadeNuvem', '24', this)">
                        <div class="opcao-titulo">A3 Nuves 24 meses</div>
                        <div class="opcao-subtitulo">Acesso bianual</div>
                        <div class="preco-destaque">R$ 379,00</div>
                    </div>
                </div>
            </div>
        </div>

    </div>

    <script>
        // Objeto global para armazenar as decisões atuais do fluxo
        let escolhas = {
            tipo: null,
            modelo: null,
            midia: null,
            validadeA3: null,
            validadeNuvem: null
        };

        function selecionarOpcao(passo, chave, valor, elemento) {
            // Remove a classe 'selecionado' dos irmãos do mesmo grupo
            const irmaos = elemento.parentNode.querySelectorAll('.card-opcao');
            irmaos.forEach(card => card.classList.remove('selecionado'));
            
            // Adiciona destaque ao card clicado
            elemento.classList.add('selecionado');

            // Salva a escolha do usuário
            escolhas[chave] = valor;

            // Gerencia os gatilhos visuais para abrir ao lado conforme as regras informadas
            const p2 = document.getElementById('passo-2');
            const p3A1 = document.getElementById('passo-3-a1');
            const p3A3 = document.getElementById('passo-3-a3');
            const p4A3 = document.getElementById('passo-4-a3');
            const p3Nuvem = document.getElementById('passo-3-nuvem');

            if (passo === 1) {
                // Ao escolher CPF ou CNPJ, abre o Passo 2 imediatamente ao lado
                p2.classList.remove('hidden');
                
                // Reseta passos subsequentes caso mude o tipo inicial depois de avançar
                p3A1.classList.add('hidden');
                p3A3.classList.add('hidden');
                p4A3.classList.add('hidden');
                p3Nuvem.classList.add('hidden');
                limparSelecoesDesde(2);
            } 
            else if (passo === 2) {
                // Esconde os fluxos antigos para renderizar o novo caminho escolhido
                p3A1.classList.add('hidden');
                p3A3.classList.add('hidden');
                p4A3.classList.add('hidden');
                p3Nuvem.classList.add('hidden');
                limparSelecoesDesde(3);

                if (valor === 'a1') {
                    p3A1.classList.remove('hidden');
                } else if (valor === 'a3') {
                    p3A3.classList.remove('hidden');
                } else if (valor === 'nuvem') {
                    p3Nuvem.classList.remove('hidden');
                }
            } 
            else if (passo === 3 && chave === 'midia') {
                // Quando seleciona Token, Cartão ou Renovação, abre as validades ao lado
                p4A3.classList.remove('hidden');
                
                // Reseta sub-valores do passo 4 se trocar a mídia no meio do caminho
                const opcoesValidade = p4A3.querySelectorAll('.card-opcao');
                opcoesValidade.forEach(card => card.classList.remove('selecionado'));
                escolhas['validadeA3'] = null;
            }

            // Scroll automático para a direita à medida que as colunas abrem
            setTimeout(() => {
                const conteiner = document.getElementById('fluxoConteiner');
                conteiner.scrollLeft = conteiner.scrollWidth;
            }, 50);
        }

        // Função auxiliar para resetar estados visuais internos caso o cliente mude de ideia no meio do fluxo
        function limparSelecoesDesde(numPasso) {
            if (numPasso <= 2) {
                document.getElementById('passo-2').querySelectorAll('.card-opcao').forEach(c => c.classList.remove('selecionado'));
                escolhas.modelo = null;
            }
            if (numPasso <= 3) {
                document.getElementById('passo-3-a3').querySelectorAll('.card-opcao').forEach(c => c.classList.remove('selecionado'));
                document.getElementById('passo-3-nuvem').querySelectorAll('.card-opcao').forEach(c => c.classList.remove('selecionado'));
                escolhas.midia = null;
                escolhas.validadeNuvem = null;
            }
            if (numPasso <= 4) {
                document.getElementById('passo-4-a3').querySelectorAll('.card-opcao').forEach(c => c.classList.remove('selecionado'));
                escolhas.validadeA3 = null;
            }
        }
    </script>
</body>
</html>
