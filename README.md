<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KUEHNE+NAGEL | Automação Pós-Sorting & Analytics</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        kn: {
                            navy: '#003366',
                            blue: '#004B93',
                            light: '#F8FAFC',
                            surface: '#FFFFFF',
                            border: '#E2E8F0',
                            accent: '#0055A5'
                        }
                    }
                }
            }
        }
    </script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body class="bg-kn-light flex h-screen overflow-hidden font-sans text-slate-800">

    <!-- ================= SIDEBAR CORPORATIVA (KUEHNE+NAGEL) ================= -->
    <aside class="w-64 bg-kn-navy text-white flex flex-col justify-between z-20 shadow-xl flex-shrink-0">
        <div class="flex-1 flex flex-col overflow-hidden">
            <div class="p-5 border-b border-white/10 flex items-center justify-between bg-[#002850]">
                <div class="flex items-center space-x-3">
                    <svg class="w-8 h-8 text-white flex-shrink-0" viewBox="0 0 100 100" fill="none" stroke="currentColor" stroke-width="8">
                        <circle cx="50" cy="50" r="42" />
                        <line x1="50" y1="20" x2="50" y2="72" />
                        <circle cx="50" cy="28" r="6" fill="currentColor" />
                        <path d="M26 62 C 26 78, 74 78, 74 62" stroke-width="8" />
                    </svg>
                    <div class="flex flex-col">
                        <span class="font-bold tracking-wider text-xs leading-tight">KUEHNE+NAGEL</span>
                        <span class="text-[9px] text-slate-300 tracking-widest uppercase font-semibold">Control Tower + Pandas</span>
                    </div>
                </div>
            </div>

            <nav id="nav-menu" class="p-3 space-y-1.5 text-xs overflow-y-auto flex-1">
                <div class="text-[9px] text-slate-400 font-bold uppercase tracking-wider px-3 pb-1 pt-2">Operação Last Mile</div>
                
                <button onclick="mudarAba('operacao')" id="btn-aba-operacao" class="w-full flex items-center space-x-3 p-3 rounded-lg bg-kn-blue text-white transition shadow-sm font-medium">
                    <i data-lucide="scan-barcode" class="w-4 h-4"></i>
                    <span>Bipagem Inteligente</span>
                </button>

                <button onclick="mudarAba('rotas')" id="btn-aba-rotas" class="w-full flex items-center space-x-3 p-3 rounded-lg hover:bg-white/5 text-slate-300 hover:text-white transition font-medium">
                    <i data-lucide="truck" class="w-4 h-4"></i>
                    <span>Resumo por Rota</span>
                </button>

                <button onclick="mudarAba('python-engine')" id="btn-aba-python-engine" class="w-full flex items-center space-x-3 p-3 rounded-lg hover:bg-white/5 text-slate-300 hover:text-white transition font-medium">
                    <i data-lucide="cpu" class="w-4 h-4 text-emerald-400"></i>
                    <span>Pipeline Python (Pandas)</span>
                </button>

                <div class="text-[9px] text-slate-400 font-bold uppercase tracking-wider px-3 pb-1 pt-5">Business Intelligence</div>
                
                <button onclick="mudarAba('graficos-geral')" id="btn-aba-graficos-geral" class="w-full flex items-center space-x-3 p-3 rounded-lg hover:bg-white/5 text-slate-300 hover:text-white transition font-medium">
                    <i data-lucide="pie-chart" class="w-4 h-4"></i>
                    <span>Visão Comparativa</span>
                </button>
            </nav>
        </div>

        <div class="p-4 border-t border-white/10 text-[11px] text-slate-300 text-center flex flex-col items-center justify-center space-y-1 bg-[#002850]">
            <i data-lucide="code-2" class="w-4 h-4 text-sky-400 mb-0.5"></i>
            <span class="font-semibold tracking-wide text-white">Desenvolvido por Nathan</span>
            <span class="text-[9px] text-slate-400">Logistics Systems v3.0 (Py)</span>
        </div>
    </aside>

    <!-- ================= CONTEÚDO PRINCIPAL ================= -->
    <main class="flex-1 flex flex-col overflow-y-auto bg-slate-50">
        
        <header class="bg-white border-b border-kn-border px-8 py-4 flex flex-wrap items-center justify-between sticky top-0 z-10 shadow-sm gap-4">
            <div>
                <h1 class="text-base font-bold text-kn-navy tracking-tight flex items-center gap-2">
                    <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                    Automação Pós-Sorting & Análise de Dados
                </h1>
                <p class="text-xs text-slate-500">Módulo Integrado JavaScript + Python Pandas Analytics</p>
            </div>
            
            <div class="flex items-center space-x-2 flex-wrap gap-y-2">
                <div class="flex items-center bg-slate-100 p-1 rounded-lg border border-slate-200 space-x-1">
                    <button onclick="exportarCSV('AM')" class="hover:bg-sky-500 hover:text-white text-slate-700 bg-white px-2.5 py-1.5 rounded text-xs font-semibold flex items-center space-x-1 transition">
                        <i data-lucide="sun" class="w-3.5 h-3.5 text-amber-500"></i>
                        <span>CSV AM</span>
                    </button>
                    <button onclick="exportarCSV('PM')" class="hover:bg-indigo-600 hover:text-white text-slate-700 bg-white px-2.5 py-1.5 rounded text-xs font-semibold flex items-center space-x-1 transition">
                        <i data-lucide="moon" class="w-3.5 h-3.5 text-indigo-500"></i>
                        <span>CSV PM</span>
                    </button>
                </div>
                <button onclick="limparBase()" class="bg-white border border-rose-200 text-rose-600 hover:bg-rose-50 px-3 py-2 rounded-lg text-xs font-semibold flex items-center space-x-1.5 transition">
                    <i data-lucide="trash-2" class="w-3.5 h-3.5"></i>
                    <span>Zerar Dados</span>
                </button>
            </div>
        </header>

        <div class="p-8 space-y-6 max-w-7xl mx-auto w-full">

            <!-- KPIS EXECUTIVOS -->
            <div class="grid grid-cols-2 md:grid-cols-6 gap-3">
                <div class="bg-white p-4 rounded-xl shadow-sm border border-kn-border border-l-4 border-l-kn-navy">
                    <span class="text-[10px] font-bold text-slate-400 uppercase tracking-wider">Total</span>
                    <div id="kpiTotal" class="text-xl font-black text-slate-800 mt-1">0</div>
                </div>
                <div class="bg-white p-4 rounded-xl shadow-sm border border-kn-border border-l-4 border-l-sky-500">
                    <span class="text-[10px] font-bold text-slate-400 uppercase tracking-wider">Despachar</span>
                    <div id="kpiDespachar" class="text-xl font-black text-sky-600 mt-1">0</div>
                </div>
                <div class="bg-white p-4 rounded-xl shadow-sm border border-kn-border border-l-4 border-l-emerald-500">
                    <span class="text-[10px] font-bold text-slate-400 uppercase tracking-wider">Em Rota</span>
                    <div id="kpiEmRota" class="text-xl font-black text-emerald-600 mt-1">0</div>
                </div>
                <div class="bg-white p-4 rounded-xl shadow-sm border border-kn-border border-l-4 border-l-amber-500">
                    <span class="text-[10px] font-bold text-slate-400 uppercase tracking-wider">No Piso</span>
                    <div id="kpiPiso" class="text-xl font-black text-amber-600 mt-1">0</div>
                </div>
                <div class="bg-white p-4 rounded-xl shadow-sm border border-kn-border border-l-4 border-l-rose-500">
                    <span class="text-[10px] font-bold text-slate-400 uppercase tracking-wider">Falha Entrega</span>
                    <div id="kpiFalha" class="text-xl font-black text-rose-600 mt-1">0</div>
                </div>
                <div class="bg-white p-4 rounded-xl shadow-sm border border-kn-border border-l-4 border-l-purple-500">
                    <span class="text-[10px] font-bold text-slate-400 uppercase tracking-wider">Solução Prob.</span>
                    <div id="kpiSolucao" class="text-xl font-black text-purple-600 mt-1">0</div>
                </div>
            </div>

            <!-- ================= ABA 1: BIPAGEM INTELIGENTE ================= -->
            <section id="aba-operacao" class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <div class="space-y-6">
                    <div class="bg-white p-6 rounded-xl shadow-sm border border-kn-border space-y-5">
                        <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                            <h2 class="text-xs font-bold text-kn-navy uppercase tracking-wider">Leitor Óptico</h2>
                            <span id="badge-ciclo" class="text-[10px] bg-kn-navy text-white px-2.5 py-1 rounded font-mono font-bold">CICLO AM</span>
                        </div>
                        <div id="feedbackAlerta" class="hidden p-3 rounded-lg text-xs font-medium border shadow-sm"></div>
                        <div class="space-y-4">
                            <div>
                                <label class="text-xs font-semibold text-slate-600 uppercase tracking-wide">Código de Barras</label>
                                <input type="text" id="barcodeInput" autofocus placeholder="Aguardando leitura..." class="w-full p-3 border border-slate-300 rounded-lg font-mono text-sm focus:ring-2 focus:ring-kn-navy focus:outline-none bg-slate-50 mt-1">
                            </div>
                            <div class="grid grid-cols-2 gap-3 pt-3 border-t border-slate-100">
                                <div>
                                    <label class="text-xs font-semibold text-slate-600">Rota / Gaiola:</label>
                                    <input type="text" id="atribuicaoInput" placeholder="Ex: Gaiola 01" class="w-full p-2.5 border border-slate-300 rounded-lg text-xs mt-1 bg-slate-50">
                                </div>
                                <div>
                                    <label class="text-xs font-semibold text-slate-600">Ciclo Ativo:</label>
                                    <select id="selectCiclo" onchange="atualizarCicloBadge()" class="w-full p-2.5 border border-slate-300 rounded-lg text-xs mt-1 bg-white font-bold text-kn-navy">
                                        <option value="AM">AM</option>
                                        <option value="PM">PM</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Tabela de Histórico -->
                <div class="bg-white p-6 rounded-xl shadow-sm border border-kn-border lg:col-span-2 space-y-4">
                    <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                        <h2 class="text-xs font-bold text-kn-navy uppercase tracking-wider">Histórico de Movimentações</h2>
                        <span id="contadorBips" class="text-xs font-semibold bg-slate-100 text-kn-navy px-3 py-1 rounded-full border">0 Pacotes</span>
                    </div>
                    <div class="overflow-x-auto max-h-[480px]">
                        <table class="w-full text-left text-xs">
                            <thead class="bg-slate-100 text-slate-600 font-bold uppercase border-b sticky top-0">
                                <tr>
                                    <th class="p-3">Pacote / ID</th>
                                    <th class="p-3">Rota / Gaiola</th>
                                    <th class="p-3">Ciclo</th>
                                    <th class="p-3">Status</th>
                                    <th class="p-3">Hora</th>
                                </tr>
                            </thead>
                            <tbody id="tabelaHistorico" class="divide-y divide-slate-100 font-mono"></tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- ================= ABA 2: RESUMO POR ROTA ================= -->
            <section id="aba-rotas" class="hidden bg-white p-6 rounded-xl shadow-sm border border-kn-border space-y-4">
                <h2 class="text-xs font-bold text-kn-navy uppercase tracking-wider border-b pb-3">Resumo Agrupado por Rota</h2>
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-xs">
                        <thead class="bg-slate-100 text-slate-600 font-bold uppercase border-b">
                            <tr>
                                <th class="p-3">Rota</th>
                                <th class="p-3">Total Pacotes</th>
                                <th class="p-3">Em Rota</th>
                                <th class="p-3">No Piso</th>
                                <th class="p-3">Despachar</th>
                            </tr>
                        </thead>
                        <tbody id="tabelaRotas" class="divide-y divide-slate-100 font-mono"></tbody>
                    </table>
                </div>
            </section>

            <!-- ================= ABA 3: PIPELINE PYTHON & PANDAS ================= -->
            <section id="aba-python-engine" class="hidden bg-white p-6 rounded-xl shadow-sm border border-emerald-200 space-y-4 bg-emerald-50/10">
                <div class="flex items-center justify-between border-b border-emerald-100 pb-3">
                    <div class="flex items-center space-x-2">
                        <i data-lucide="cpu" class="w-5 h-5 text-emerald-600"></i>
                        <h2 class="text-xs font-bold text-emerald-900 uppercase tracking-wider">Módulo de Análise de Dados com Python (Pandas)</h2>
                    </div>
                    <span class="bg-emerald-600 text-white text-[10px] px-2 py-0.5 rounded font-mono font-bold">Backend Script Ready</span>
                </div>
                <p class="text-xs text-slate-600">
                    Abaixo está o script oficial em Python utilizando as bibliotecas <strong>Pandas</strong> e <strong>NumPy</strong> configurado para processar os arquivos de log da operação Last Mile, remover duplicidades, agregar volumes por rota e gerar relatórios consolidados em Excel/CSV de forma automatizada:
                </p>
                <div class="relative">
                    <pre class="bg-slate-900 text-emerald-400 p-4 rounded-lg font-mono text-[11px] overflow-x-auto leading-relaxed"><code># =====================================================================
# KUEHNE+NAGEL - PIPELINE DE PROCESSAMENTO LAST MILE (PANDAS + NUMPY)
# Desenvolvido para automação de reconciliação pós-sorting
# =====================================================================
import pandas as pd
import numpy as np
from datetime import datetime

def processar_base_logistica(caminho_arquivo_csv):
    # Carregando a base de dados exportada do sistema
    df = pd.read_csv(caminho_arquivo_csv)
    
    # Limpeza e Tratamento de Dados (Data Cleaning)
    df.drop_duplicates(subset=['id'], keep='last', inplace=True)
    df['status'] = df['status'].fillna('NULO').str.upper()
    df['rota'] = df['rota'].fillna('SEM ROTA').str.strip()
    
    # Agrupamento e Análise Estatística por Rota com Pandas
    resumo_rotas = df.groupby(['ciclo', 'rota']).agg(
        total_pacotes=('id', 'count'),
        em_rota=('status', lambda x: (x == 'EM_ROTA_DE_ENTREGA').sum()),
        no_piso=('status', lambda x: (x == 'FICOU_NO_PISO').sum()),
        falhas=('status', lambda x: (x == 'FALHA_NA_ENTREGA').sum())
    ).reset_index()
    
    # Ordenação por volume total de pacotes
    resumo_rotas = resumo_rotas.sort_values(by='total_pacotes', ascending=False)
    
    # Exportação de Relatórios Tratados
    timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
    nome_relatorio = f"relatorio_analítico_last_mile_{timestamp}.xlsx"
    
    with pd.ExcelWriter(nome_relatorio, engine='openpyxl') as writer:
        df.to_excel(writer, sheet_name='Base Tratada', index=False)
        resumo_rotas.to_excel(writer, sheet_name='KPIs por Rota', index=False)
        
    print(f"[SUCESSO] Relatório gerado e processado via Pandas: {nome_relatorio}")
    return resumo_rotas

# Exemplo de execução local:
# processar_base_logistica('dados_bipagem.csv')</code></pre>
                </div>
            </section>

            <!-- ================= ABA 4: BI / GRÁFICOS ================= -->
            <section id="aba-graficos-geral" class="hidden space-y-6">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-white p-5 rounded-xl border border-kn-border shadow-sm">
                        <h3 class="text-xs font-bold text-kn-navy uppercase tracking-wider mb-4">Distribuição Geral de Status</h3>
                        <canvas id="chartGeralStatus" class="max-h-64"></canvas>
                    </div>
                    <div class="bg-white p-5 rounded-xl border border-kn-border shadow-sm">
                        <h3 class="text-xs font-bold text-kn-navy uppercase tracking-wider mb-4">Volume Ciclo AM vs PM</h3>
                        <canvas id="chartGeralCiclos" class="max-h-64"></canvas>
                    </div>
                </div>
            </section>

        </div>
    </main>

    <!-- ================= SCRIPT DE CONTROLE JAVASCRIPT ================= -->
    <script>
        let pacotes = JSON.parse(localStorage.getItem('kn_pacotes')) || [];
        let charts = {};

        document.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            atualizarCicloBadge();
            renderizarTabela();
            atualizarKPIs();
            renderizarResumoRotas();
            
            document.getElementById('barcodeInput').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    processarBip(this.value.trim());
                    this.value = '';
                }
            });
        });

        function mudarAba(abaId) {
            ['aba-operacao', 'aba-rotas', 'aba-python-engine', 'aba-graficos-geral'].forEach(id => {
                document.getElementById(id).classList.add('hidden');
            });
            document.getElementById(`aba-${abaId}`).classList.remove('hidden');
            
            document.querySelectorAll('nav button').forEach(btn => btn.classList.remove('bg-kn-blue', 'text-white'));
            document.getElementById(`btn-aba-${abaId}`).classList.add('bg-kn-blue', 'text-white');
            if(abaId === 'graficos-geral') renderizarGraficos();
        }

        function atualizarCicloBadge() {
            const ciclo = document.getElementById('selectCiclo').value;
            const badge = document.getElementById('badge-ciclo');
            badge.innerText = `CICLO ${ciclo}`;
            badge.className = `text-[10px] ${ciclo === 'AM' ? 'bg-amber-500' : 'bg-indigo-600'} text-white px-2.5 py-1 rounded font-mono font-bold`;
        }

        function processarBip(codigo) {
            if (!codigo) return;
            const ciclo = document.getElementById('selectCiclo').value;
            const rota = document.getElementById('atribuicaoInput').value.trim() || 'Sem Rota';
            const index = pacotes.findIndex(p => p.id === codigo);
            const agora = new Date().toLocaleTimeString('pt-BR', { hour: '2-digit', minute: '2-digit', second: '2-digit' });

            if (index === -1) {
                pacotes.unshift({ id: codigo, rota, ciclo, status: 'EM_ROTA_DE_ENTREGA', hora: agora });
                exibirAlerta(`Pacote ${codigo} adicionado: EM ROTA`, 'sucesso');
            } else {
                pacotes[index].status = 'FICOU_NO_PISO';
                pacotes[index].hora = agora;
                if(rota !== 'Sem Rota') pacotes[index].rota = rota;
                exibirAlerta(`Pacote ${codigo} atualizado: FICOU NO PISO`, 'aviso');
            }
            salvarEAtualizar();
        }

        function exibirAlerta(mensagem, tipo) {
            const alerta = document.getElementById('feedbackAlerta');
            alerta.className = `p-3 rounded-lg text-xs font-medium border block ${tipo === 'sucesso' ? 'bg-emerald-50 border-emerald-200 text-emerald-800' : 'bg-amber-50 border-amber-200 text-amber-800'}`;
            alerta.innerText = mensagem;
            setTimeout(() => alerta.classList.add('hidden'), 3500);
        }

        function salvarEAtualizar() {
            localStorage.setItem('kn_pacotes', JSON.stringify(pacotes));
            renderizarTabela();
            atualizarKPIs();
            renderizarResumoRotas();
        }

        function atualizarKPIs() {
            document.getElementById('kpiTotal').innerText = pacotes.length;
            document.getElementById('kpiDespachar').innerText = pacotes.filter(p => p.status === 'DESPACHAR').length;
            document.getElementById('kpiEmRota').innerText = pacotes.filter(p => p.status === 'EM_ROTA_DE_ENTREGA').length;
            document.getElementById('kpiPiso').innerText = pacotes.filter(p => p.status === 'FICOU_NO_PISO').length;
            document.getElementById('kpiFalha').innerText = pacotes.filter(p => p.status === 'FALHA_NA_ENTREGA').length;
            document.getElementById('kpiSolucao').innerText = pacotes.filter(p => p.status === 'SOLUCAO_DE_PROBLEMA').length;
            document.getElementById('contadorBips').innerText = `${pacotes.length} Pacotes`;
        }

        function renderizarTabela() {
            const tbody = document.getElementById('tabelaHistorico');
            tbody.innerHTML = '';
            pacotes.forEach(p => {
                tbody.innerHTML += `
                    <tr class="hover:bg-slate-50 transition">
                        <td class="p-3 font-bold text-kn-navy">${p.id}</td>
                        <td class="p-3">${p.rota}</td>
                        <td class="p-3"><span class="px-2 py-0.5 rounded text-[10px] font-bold ${p.ciclo === 'AM' ? 'bg-amber-100 text-amber-800' : 'bg-indigo-100 text-indigo-800'}">${p.ciclo}</span></td>
                        <td class="p-3 font-semibold">${p.status}</td>
                        <td class="p-3 text-slate-500">${p.hora}</td>
                    </tr>`;
            });
        }

        function renderizarResumoRotas() {
            const tbody = document.getElementById('tabelaRotas');
            tbody.innerHTML = '';
            const rotasMap = {};
            
            pacotes.forEach(p => {
                if(!rotasMap[p.rota]) rotasMap[p.rota] = { total: 0, emRota: 0, piso: 0, despachar: 0 };
                rotasMap[p.rota].total++;
                if(p.status === 'EM_ROTA_DE_ENTREGA') rotasMap[p.rota].emRota++;
                if(p.status === 'FICOU_NO_PISO') rotasMap[p.rota].piso++;
                if(p.status === 'DESPACHAR') rotasMap[p.rota].despachar++;
            });

            for(let [rota, dados] of Object.entries(rotasMap)) {
                tbody.innerHTML += `
                    <tr class="hover:bg-slate-50">
                        <td class="p-3 font-bold text-kn-navy">${rota}</td>
                        <td class="p-3 font-semibold">${dados.total}</td>
                        <td class="p-3 text-emerald-600">${dados.emRota}</td>
                        <td class="p-3 text-amber-600">${dados.piso}</td>
                        <td class="p-3 text-sky-600">${dados.despachar}</td>
                    </tr>`;
            }
        }

        function exportarCSV(filtroCiclo) {
            let csv = 'ID,Rota,Ciclo,Status,Hora\n';
            pacotes.filter(p => filtroCiclo === 'TODOS' || p.ciclo === filtroCiclo).forEach(p => {
                csv += `${p.id},${p.rota},${p.ciclo},${p.status},${p.hora}\n`;
            });
            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = `pacotes_${filtroCiclo}.csv`;
            link.click();
        }

        function limparBase() {
            if(confirm("Deseja realmente zerar todos os dados salvos?")) {
                pacotes = [];
                salvarEAtualizar();
            }
        }

        function renderizarGraficos() {
            if(charts.geralStatus) charts.geralStatus.destroy();
            const ctx1 = document.getElementById('chartGeralStatus').getContext('2d');
            charts.geralStatus = new Chart(ctx1, {
                type: 'doughnut',
                data: {
                    labels: ['Em Rota', 'No Piso', 'Despachar', 'Falha'],
                    datasets: [{
                        data: [
                            pacotes.filter(p => p.status === 'EM_ROTA_DE_ENTREGA').length,
                            pacotes.filter(p => p.status === 'FICOU_NO_PISO').length,
                            pacotes.filter(p => p.status === 'DESPACHAR').length,
                            pacotes.filter(p => p.status === 'FALHA_NA_ENTREGA').length
                        ],
                        backgroundColor: ['#10B981', '#F59E0B', '#0EA5E9', '#EF4444']
                    }]
                },
                options: { responsive: true, maintainAspectRatio: false }
            });
        }
    </script>
</body>
</html>
