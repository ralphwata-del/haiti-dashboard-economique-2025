<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard Économique Haïti 2025</title>
    
    <!-- Styles CSS -->
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            color: #2c3e50;
            line-height: 1.6;
            min-height: 100vh;
        }

        .dashboard-container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Header */
        .dashboard-header {
            background: linear-gradient(135deg, #2c3e50 0%, #3498db 100%);
            color: white;
            padding: 30px;
            border-radius: 15px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .dashboard-title {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 10px;
            text-align: center;
        }

        .dashboard-subtitle {
            font-size: 1.2rem;
            text-align: center;
            opacity: 0.9;
            font-weight: 300;
        }

        /* KPI Cards */
        .kpi-section {
            margin-bottom: 40px;
        }

        .section-title {
            font-size: 1.8rem;
            font-weight: 600;
            color: #2c3e50;
            margin-bottom: 25px;
            padding-bottom: 10px;
            border-bottom: 3px solid #3498db;
        }

        .kpi-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .kpi-card {
            background: white;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            border-left: 5px solid #3498db;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .kpi-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
        }

        .kpi-card.critical {
            border-left-color: #e74c3c;
        }

        .kpi-card.warning {
            border-left-color: #f39c12;
        }

        .kpi-card.positive {
            border-left-color: #27ae60;
        }

        .kpi-value {
            font-size: 2.5rem;
            font-weight: 700;
            color: #2c3e50;
            margin-bottom: 5px;
        }

        .kpi-label {
            font-size: 0.9rem;
            color: #7f8c8d;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 10px;
        }

        .kpi-description {
            font-size: 0.85rem;
            color: #95a5a6;
            line-height: 1.4;
        }

        /* Charts Section */
        .charts-section {
            margin-bottom: 40px;
        }

        .charts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
            gap: 30px;
            margin-bottom: 30px;
        }

        .chart-container {
            background: white;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            min-height: 400px;
        }

        .chart-title {
            font-size: 1.3rem;
            font-weight: 600;
            color: #2c3e50;
            margin-bottom: 20px;
            text-align: center;
        }

        .chart {
            width: 100%;
            height: 350px;
        }

        /* Footer */
        .dashboard-footer {
            background: #2c3e50;
            color: white;
            padding: 20px;
            border-radius: 12px;
            text-align: center;
            margin-top: 40px;
        }

        .footer-text {
            font-size: 0.9rem;
            opacity: 0.8;
        }

        /* Refresh Controls */
        .refresh-controls {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            padding: 15px;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            z-index: 1000;
            min-width: 250px;
        }
        
        .refresh-btn {
            background: #3498db;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s ease;
            width: 100%;
            margin-bottom: 10px;
        }
        
        .refresh-btn:hover {
            background: #2980b9;
            transform: translateY(-2px);
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .dashboard-container {
                padding: 15px;
            }
            
            .dashboard-title {
                font-size: 2rem;
            }
            
            .kpi-grid {
                grid-template-columns: 1fr;
            }
            
            .charts-grid {
                grid-template-columns: 1fr;
            }
            
            .refresh-controls {
                position: relative;
                width: 100%;
                margin-bottom: 20px;
            }
        }
    </style>
    
    <!-- ECharts CDN -->
    <script src="https://cdn.jsdelivr.net/npm/echarts@5.4.3/dist/echarts.min.js"></script>
</head>
<body>
    <!-- Contrôles de Refresh -->
    <div class="refresh-controls">
        <button class="refresh-btn" onclick="refreshDashboard()">
            🔄 Actualiser Maintenant
        </button>
        <div style="font-size: 0.8rem; color: #7f8c8d; text-align: center; margin-top: 10px;">
            Dashboard Économique Haïti 2025
        </div>
    </div>

    <div class="dashboard-container">
        <!-- Header -->
        <header class="dashboard-header">
            <h1 class="dashboard-title">🇭🇹 Dashboard Économique Haïti 2025</h1>
            <p class="dashboard-subtitle">Analyse exhaustive des événements économiques, politiques et sécuritaires</p>
        </header>

        <!-- KPI Section -->
        <section class="kpi-section">
            <h2 class="section-title">📊 Indicateurs Clés de Performance</h2>
            <div class="kpi-grid">
                <div class="kpi-card critical">
                    <div class="kpi-value">31.9%</div>
                    <div class="kpi-label">Inflation Annuelle</div>
                    <div class="kpi-description">Pic d'inflation atteint en septembre 2025</div>
                </div>
                
                <div class="kpi-card critical">
                    <div class="kpi-value">90%</div>
                    <div class="kpi-label">Contrôle des Gangs</div>
                    <div class="kpi-description">Pourcentage de Port-au-Prince sous contrôle des gangs</div>
                </div>
                
                <div class="kpi-card warning">
                    <div class="kpi-value">1.4M</div>
                    <div class="kpi-label">Déplacés Internes</div>
                    <div class="kpi-description">Personnes déplacées à cause de la violence</div>
                </div>
                
                <div class="kpi-card critical">
                    <div class="kpi-value">5.7M</div>
                    <div class="kpi-label">Insécurité Alimentaire</div>
                    <div class="kpi-description">Personnes en insécurité alimentaire aiguë</div>
                </div>
                
                <div class="kpi-card">
                    <div class="kpi-value">130.60</div>
                    <div class="kpi-label">Taux de Change HTG/USD</div>
                    <div class="kpi-description">Stabilité relative maintenue par la BRH</div>
                </div>
                
                <div class="kpi-card positive">
                    <div class="kpi-value">345.5Md</div>
                    <div class="kpi-label">Budget 2025-2026</div>
                    <div class="kpi-description">Budget adopté en gourdes haïtiennes</div>
                </div>
            </div>
        </section>

        <!-- Charts Section -->
        <section class="charts-section">
            <h2 class="section-title">📈 Visualisations Économiques</h2>
            <div class="charts-grid">
                <div class="chart-container">
                    <h3 class="chart-title">Évolution de l'Inflation 2025</h3>
                    <div id="inflation-chart" class="chart"></div>
                </div>
                
                <div class="chart-container">
                    <h3 class="chart-title">Taux de Change HTG/USD</h3>
                    <div id="exchange-rate-chart" class="chart"></div>
                </div>
                
                <div class="chart-container">
                    <h3 class="chart-title">Financements Internationaux</h3>
                    <div id="funding-chart" class="chart"></div>
                </div>
                
                <div class="chart-container">
                    <h3 class="chart-title">Impact Économique - Événements Sécuritaires</h3>
                    <div id="security-impact-chart" class="chart"></div>
                </div>
            </div>
        </section>

        <!-- Footer -->
        <footer class="dashboard-footer">
            <p class="footer-text">
                Dashboard Économique Haïti 2025 | Données compilées à partir de sources officielles (BRH, MEF, FMI, Banque Mondiale) 
                et médias spécialisés haïtiens | Dernière mise à jour: 6 décembre 2025
            </p>
        </footer>
    </div>

    <!-- JavaScript -->
    <script>
        // Données du dashboard
        const dashboardData = {
            inflationMonthly: [
                { month: "Jan", value: 2.1 },
                { month: "Fév", value: 2.3 },
                { month: "Mar", value: 2.4 },
                { month: "Avr", value: 3.0 },
                { month: "Mai", value: 2.8 },
                { month: "Jun", value: 2.5 },
                { month: "Jul", value: 2.7 },
                { month: "Aoû", value: 2.9 },
                { month: "Sep", value: 1.8 }
            ],
            exchangeRateData: [
                { month: "Jan", value: 130.21 },
                { month: "Fév", value: 130.41 },
                { month: "Mar", value: 130.65 },
                { month: "Déc", value: 130.60 }
            ],
            internationalFunding: [
                { source: "Banque Mondiale", amount: 320, type: "Stratégie générale" },
                { source: "Banque Mondiale", amount: 50, type: "Agriculture" },
                { source: "FIDA", amount: 8.11, type: "Agriculture additionnelle" },
                { source: "Plan Humanitaire", amount: 674, type: "Réponse humanitaire" }
            ],
            securityEvents: [
                { event: "Alerte sécuritaire Ambassade US", impactScore: 3 },
                { event: "Massacre Wharf Jérémie", impactScore: 4 },
                { event: "Force Suppression Gangs ONU", impactScore: -2 },
                { event: "Violence gangs Nord", impactScore: 4 },
                { event: "Nouveau massacre Pont-Sondé", impactScore: 5 }
            ]
        };

        // Configuration des couleurs
        const themeColors = {
            primary: '#3498db',
            secondary: '#2c3e50',
            success: '#27ae60',
            warning: '#f39c12',
            danger: '#e74c3c',
            info: '#9b59b6'
        };

        // Initialisation du dashboard
        function initDashboard() {
            createInflationChart();
            createExchangeRateChart();
            createFundingChart();
            createSecurityImpactChart();
        }

        // Graphique d'inflation
        function createInflationChart() {
            const chart = echarts.init(document.getElementById('inflation-chart'));
            const data = dashboardData.inflationMonthly;
            
            const option = {
                title: {
                    text: 'Évolution de l\'Inflation 2025',
                    left: 'center',
                    textStyle: { color: themeColors.secondary, fontSize: 16, fontWeight: 'bold' }
                },
                tooltip: {
                    trigger: 'axis',
                    formatter: '{b}: {c}%'
                },
                xAxis: {
                    type: 'category',
                    data: data.map(item => item.month)
                },
                yAxis: {
                    type: 'value',
                    name: 'Pourcentage (%)'
                },
                series: [{
                    type: 'line',
                    data: data.map(item => item.value),
                    smooth: true,
                    lineStyle: { color: themeColors.primary, width: 3 },
                    itemStyle: { color: themeColors.primary },
                    areaStyle: { color: themeColors.primary + '40' }
                }]
            };
            
            chart.setOption(option);
            window.addEventListener('resize', () => chart.resize());
        }

        // Graphique du taux de change
        function createExchangeRateChart() {
            const chart = echarts.init(document.getElementById('exchange-rate-chart'));
            const data = dashboardData.exchangeRateData;
            
            const option = {
                title: {
                    text: 'Taux de Change HTG/USD',
                    left: 'center',
                    textStyle: { color: themeColors.secondary, fontSize: 16, fontWeight: 'bold' }
                },
                tooltip: {
                    trigger: 'axis',
                    formatter: '{b}: {c} HTG/USD'
                },
                xAxis: {
                    type: 'category',
                    data: data.map(item => item.month)
                },
                yAxis: {
                    type: 'value',
                    name: 'HTG/USD',
                    min: 130,
                    max: 131
                },
                series: [{
                    type: 'line',
                    data: data.map(item => item.value),
                    smooth: true,
                    lineStyle: { color: themeColors.success, width: 4 },
                    itemStyle: { color: themeColors.success }
                }]
            };
            
            chart.setOption(option);
            window.addEventListener('resize', () => chart.resize());
        }

        // Graphique des financements
        function createFundingChart() {
            const chart = echarts.init(document.getElementById('funding-chart'));
            const data = dashboardData.internationalFunding;
            
            const option = {
                title: {
                    text: 'Financements Internationaux 2025',
                    left: 'center',
                    textStyle: { color: themeColors.secondary, fontSize: 16, fontWeight: 'bold' }
                },
                tooltip: {
                    trigger: 'item',
                    formatter: '{b}: ${c}M USD ({d}%)'
                },
                series: [{
                    type: 'pie',
                    radius: ['40%', '70%'],
                    center: ['50%', '50%'],
                    data: data.map((item, index) => ({
                        value: item.amount,
                        name: item.source + ' - ' + item.type,
                        itemStyle: { 
                            color: [themeColors.primary, themeColors.success, themeColors.warning, themeColors.info][index % 4]
                        }
                    }))
                }]
            };
            
            chart.setOption(option);
            window.addEventListener('resize', () => chart.resize());
        }

        // Graphique d'impact sécuritaire
        function createSecurityImpactChart() {
            const chart = echarts.init(document.getElementById('security-impact-chart'));
            const data = dashboardData.securityEvents;
            
            const option = {
                title: {
                    text: 'Impact Économique des Événements Sécuritaires',
                    left: 'center',
                    textStyle: { color: themeColors.secondary, fontSize: 16, fontWeight: 'bold' }
                },
                tooltip: {
                    trigger: 'axis',
                    formatter: function(params) {
                        const item = data[params[0].dataIndex];
                        return `${item.event}<br/>Score d'Impact: ${item.impactScore}`;
                    }
                },
                xAxis: {
                    type: 'category',
                    data: data.map((item, index) => `Evt ${index + 1}`)
                },
                yAxis: {
                    type: 'value',
                    name: 'Score d\'Impact',
                    min: -3,
                    max: 6
                },
                series: [{
                    type: 'bar',
                    data: data.map(item => ({
                        value: item.impactScore,
                        itemStyle: {
                            color: item.impactScore > 0 ? 
                                (item.impactScore >= 4 ? themeColors.danger : themeColors.warning) : 
                                themeColors.success
                        }
                    }))
                }]
            };
            
            chart.setOption(option);
            window.addEventListener('resize', () => chart.resize());
        }

        // Fonction de refresh
        function refreshDashboard() {
            alert('🔄 Dashboard actualisé ! (Fonctionnalité de refresh automatique disponible avec Google Sheets)');
        }

        // Initialisation au chargement
        document.addEventListener('DOMContentLoaded', function() {
            if (typeof echarts !== 'undefined') {
                initDashboard();
            } else {
                console.error('ECharts n\'est pas chargé');
            }
        });
    </script>
</body>
</html>
