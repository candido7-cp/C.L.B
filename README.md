<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Power Store - Suplementos e Farmácia</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Roboto:wght@400;700;900&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        gym: '#0d0d1a',
                        gymLight: '#16162b',
                        accent: '#e63946',
                    },
                    fontFamily: {
                        title: ['Bebas Neue', 'sans-serif'],
                        body: ['Roboto', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    
    <style>
        body {
            background-color: #0a0a12;
            background-image: 
                radial-gradient(circle at 0% 0%, rgba(230, 57, 70, 0.08) 0%, transparent 50%),
                radial-gradient(circle at 100% 100%, rgba(0, 212, 255, 0.08) 0%, transparent 50%);
            font-family: 'Roboto', sans-serif;
        }
        
        /* ANIMAÇÕES GERAIS */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes pulse-glow {
            0%, 100% { box-shadow: 0 0 15px rgba(230, 57, 70, 0.5); }
            50% { box-shadow: 0 0 25px rgba(230, 57, 70, 0.8); }
        }
        
        .animate-fade-in {
            animation: fadeIn 0.5s ease forwards;
        }
        
        /* ESTILO DAS ABAS */
        .tab-btn {
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            border-bottom: 3px solid transparent;
            position: relative;
        }
        .tab-btn::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            width: 0;
            height: 3px;
            background: #e63946;
            transition: all 0.4s ease;
        }
        .tab-btn.active::after {
            width: 100%;
            left: 0;
        }
        .tab-btn.active {
            color: #ffffff;
            transform: translateY(-3px);
        }

        /* CARDS DOS PRODUTOS */
        .product-card {
            border: 1px solid rgba(255,255,255,0.1);
            background: linear-gradient(145deg, #16162b, #0d0d1a);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
            overflow: hidden;
        }
        .product-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(230, 57, 70, 0.08), transparent);
            transition: 0.6s;
        }
        .product-card:hover::before {
            left: 100%;
        }
        .product-card:hover {
            transform: translateY(-8px) scale(1.02);
            border-color: rgba(230, 57, 70, 0.5);
            box-shadow: 0 15px 35px rgba(0,0,0,0.5), 0 0 20px rgba(230, 57, 70, 0.2);
        }

        /* BOTÕES */
        .btn-beneficios {
            transition: all 0.3s ease;
            background: linear-gradient(145deg, #2d3748, #1a202c);
        }
        .btn-beneficios:hover {
            background: linear-gradient(145deg, #4a5568, #2d3748);
            transform: scale(1.05);
        }
        
        .btn-quantidade {
            transition: all 0.2s ease;
        }
        .btn-quantidade:hover {
            transform: scale(1.15);
        }
        .btn-plus {
            animation: pulse-glow 2s infinite;
        }

        /* MODAIS */
        .modal-content {
            animation: fadeIn 0.3s ease;
        }

        /* ICONE CARRINHO */
        #cartBtn {
            transition: all 0.3s ease;
        }
        #cartBtn:hover {
            transform: rotate(5deg) scale(1.1);
        }
        #cartCount {
            transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }
        #cartCount.update {
            animation: pulse 0.5s ease;
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.3); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body class="text-gray-200 min-h-screen">

    <!-- CABEÇALHO -->
    <header class="bg-gym/90 backdrop-blur-md sticky top-0 z-50 border-b border-gray-800 shadow-lg">
        <div class="max-w-7xl mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <!-- AQUI ESTÁ A IMAGEM SUBSTITUINDO A LETRA P -->
                <div class="w-14 h-14 rounded-full overflow-hidden shadow-lg shadow-accent/30 border-2 border-accent">
                    <img src="https://i.postimg.cc/BQ2fX1HY/IMG-20260612-WA0000.jpg" alt="Logo Power Store" class="w-full h-full object-cover">
                </div>
                <h1 class="text-4xl font-title tracking-wider text-white">POWER <span class="text-accent">STORE</span></h1>
            </div>
            
            <!-- BOTÃO CARRINHO -->
            <button id="cartBtn" class="relative bg-gymLight hover:bg-accent/20 transition-colors px-4 py-2 rounded-full flex items-center gap-2">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
                </svg>
                <span id="cartCount" class="absolute -top-2 -right-2 bg-white text-gym text-xs font-bold w-7 h-7 flex items-center justify-center rounded-full text-lg">0</span>
            </button>
        </div>
    </header>

    <main class="max-w-5xl mx-auto px-4 py-8">

        <!-- ABAS DE CATEGORIAS -->
        <div class="flex justify-center mb-10 border-b border-gray-800">
            <button class="tab-btn active px-8 py-4 text-2xl font-title tracking-wider text-gray-400 hover:text-white transition" data-category="landerlan">
                LANDERLAN
            </button>
            <button class="tab-btn px-8 py-4 text-2xl font-title tracking-wider text-gray-400 hover:text-white transition" data-category="neopharma">
                NEOPHARMA
            </button>
            <button class="tab-btn px-8 py-4 text-2xl font-title tracking-wider text-gray-400 hover:text-white transition" data-category="max">
                MAX
            </button>
        </div>

        <!-- ÁREA DOS PRODUTOS -->
        <div id="productsContainer" class="space-y-6">
            <!-- Produtos aparecem aqui -->
        </div>

    </main>

    <!-- MODAL BENEFÍCIOS -->
    <div id="benefitsModal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden items-center justify-center p-4">
        <div class="modal-content bg-gymLight border border-gray-700 rounded-2xl max-w-md w-full p-6 relative shadow-2xl">
            <button onclick="closeBenefits()" class="absolute top-4 right-4 text-gray-400 hover:text-white text-2xl transition hover:rotate-90">&times;</button>
            <h3 id="benefitTitle" class="text-2xl font-title text-accent mb-4"></h3>
            <p id="benefitText" class="text-gray-300 leading-relaxed mb-4 text-justify"></p>
            <button onclick="closeBenefits()" class="w-full bg-accent hover:bg-red-700 text-white font-bold py-3 rounded-lg transition transform hover:scale-105 shadow-lg shadow-accent/30">Entendi</button>
        </div>
    </div>

    <!-- MODAL CARRINHO -->
    <div id="cartModal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden items-center justify-center p-4">
        <div class="modal-content bg-gymLight border border-gray-700 rounded-2xl max-w-lg w-full p-6 relative max-h-[90vh] overflow-y-auto shadow-2xl">
            <button onclick="closeCart()" class="absolute top-4 right-4 text-gray-400 hover:text-white text-2xl transition hover:rotate-90">&times;</button>
            <h2 class="text-3xl font-title text-white mb-6">SEU PEDIDO</h2>
            
            <div id="cartItems" class="space-y-3 mb-6">
                <p class="text-gray-500 text-center italic">Carrinho vazio...</p>
            </div>

            <div class="border-t border-gray-700 pt-4">
                <div class="flex justify-between text-xl font-bold mb-6">
                    <span>TOTAL:</span>
                    <span id="cartTotal" class="text-accent">R$ 0,00</span>
                </div>

                <button id="checkoutBtn" onclick="finalizeOrder()" class="w-full bg-accent hover:bg-red-700 text-white font-bold py-4 rounded-xl text-lg uppercase tracking-wider transition transform hover:scale-105 shadow-lg shadow-accent/30">
                    FINALIZAR COMPRA
                </button>
            </div>
        </div>
    </div>

    <footer class="mt-12 py-6 text-center text-gray-500 text-sm">
        <p>&copy; 2025 Power Store - Qualidade e Performance</p>
    </footer>

    <script>
        const phone = "5585920076331";

        const products = {
            landerlan: [
                { 
                    name: "DURATESTON", 
                    price: 220.00, 
                    benefits: "O Durateston é um medicamento que contém quatro ésteres de testosterona, proporcionando uma ação rápida e prolongada no organismo. É indicado para reposição hormonal em homens com deficiência ou ausência de testosterona endógena. Promove aumento da massa muscular, força, energia, libido e melhora do bem-estar geral, além de auxiliar na recuperação física e performance atlética quando utilizado sob orientação."
                },
                { 
                    name: "ENANTATO", 
                    price: 220.00, 
                    benefits: "O Enantato de Testosterona é um hormônio anabolizante de longa duração, ideal para ciclos de ganho de massa muscular e força. Ele aumenta a síntese de proteínas, melhora a retenção de nitrogênio e estimula a produção de glóbulos vermelhos, resultando em maior resistência, disposição e recuperação mais rápida após os treinos intensos."
                },
                { 
                    name: "MASTERON", 
                    price: 220.00, 
                    benefits: "O Masteron (Drostanolona) é conhecido por suas propriedades anabólicas moderadas e fortes efeitos antiestrogênicos. É muito utilizado em fases de definição muscular, pois ajuda a reduzir a retenção de líquidos, deixando o corpo mais seco, duro e com aparência mais vascularizada. Também aumenta a dureza muscular e a densidade."
                },
                { 
                    name: "ENAN DE TREMBO", 
                    price: 220.00, 
                    benefits: "O Enantato de Trembolona é um dos esteroides mais potentes e eficazes disponíveis. Ele promove um ganho expressivo de massa muscular magra, aumenta a força, a vascularização e acelera a queima de gordura corporal. Também melhora a capacidade de recuperação e a performance nos treinos, sendo muito utilizado em ciclos de volume e definição."
                },
                { 
                    name: "DECA", 
                    price: 220.00, 
                    benefits: "O Deca-Durabolin (Nandrolona) é famoso por promover ganho de massa muscular de qualidade, força e resistência. Um dos seus maiores benefícios é a lubrificação das articulações, aliviando dores e lesões, além de auxiliar na recuperação de tecidos. Também estimula a produção de glóbulos vermelhos e melhora o apetite."
                },
                { 
                    name: "HEMOGENIN", 
                    price: 170.00, 
                    benefits: "O Hemogenin é um estimulante potente da eritropoiese, ou seja, aumenta significativamente a produção de glóbulos vermelhos e hemoglobina no sangue. Isso resulta em maior transporte de oxigênio para os músculos, aumentando a resistência física, retardando a fadiga e melhorando a performance aeróbica e anaeróbica."
                },
                { 
                    name: "OXANDROLONA 0.5 MG", 
                    price: 260.00, 
                    benefits: "A Oxandrolona é um esteroide oral muito popular por ser suave e altamente eficaz. Ela promove ganho de massa muscular magra, aumenta a força e ajuda na preservação do músculo durante dietas de baixo calórico. Possui baixa conversão em estrogênio, causando pouca retenção hídrica, ideal para definição, qualidade muscular e dureza."
                }
            ],
            neopharma: [
                { 
                    name: "DURATESTON", 
                    price: 180.00, 
                    benefits: "Combinação de quatro ésteres de testosterona que garante liberação rápida e sustentada no organismo. Ideal para reposição hormonal, aumenta a libido, energia, massa muscular, força e melhora o humor e a qualidade de vida. Indicado para quem busca resultados consistentes e bem-estar geral."
                },
                { 
                    name: "DECA", 
                    price: 180.00, 
                    benefits: "Nandrolona Decanoato excelente para ganho de massa muscular, força e recuperação. Atua na proteção e lubrificação das articulações, aliviando dores e inflamações. Promove aumento da síntese proteica e melhora da performance atlética, sendo uma das opções mais seguras e populares no mercado."
                },
                { 
                    name: "ENANTATO", 
                    price: 180.00, 
                    benefits: "Testosterona Enantato de ação prolongada, perfeito para ciclos de manutenção e volume. Estimula o crescimento muscular, aumento da força, densidade óssea e disposição. Mantém níveis hormonais estáveis ao longo do tempo, facilitando o planejamento e resultados previsíveis."
                },
                { 
                    name: "ENAN DE TREMBO", 
                    price: 180.00, 
                    benefits: "Trembolona Enantato é um produto de alta potência anabólica. Promove ganho rápido de massa magra, aumento da vascularização, dureza muscular e queima de gordura. Aumenta a capacidade de treinamento e recuperação, sendo indicado para usuários que buscam resultados expressivos e definição avançada."
                },
                { 
                    name: "CIPIONATO", 
                    price: 180.00, 
                    benefits: "Similar ao Enantato, o Cipionato de Testosterona tem ação prolongada e estável. Excelente para ganho de massa, força e reposição hormonal. Melhora a disposição, libido, recuperação e qualidade de vida, com boa tolerabilidade e resultados consistentes."
                },
                { 
                    name: "PROPIONATO", 
                    price: 180.00, 
                    benefits: "Testosterona Propionato de ação rápida e curta duração. Ideal para quem quer resultados mais imediatos, maior controle hormonal e menos retenção de líquidos. Aumenta a força, massa magra, energia e vascularização, muito utilizado em ciclos de definição."
                },
                { 
                    name: "TREMBO ACETATO", 
                    price: 180.00, 
                    benefits: "Versão de ação rápida da Trembolona, com efeitos intensos e rápidos. Promove secagem muscular acentuada, aumento da dureza, vascularização e queima de gordura. Potencializa a força e a performance, sendo muito usada em fases pré-competição ou definição."
                },
                { 
                    name: "MASTERON", 
                    price: 180.00, 
                    benefits: "Drostanolona Propionato ideal para fase de corte e definição. Reduz a retenção hídrica, aumenta a dureza e a densidade muscular, deixa a pele mais fina e realça a vascularização. Possui ação antiestrogênica, ajudando a evitar efeitos colaterais indesejados."
                },
                { 
                    name: "STANOZOLOL", 
                    price: 180.00, 
                    benefits: "O Stanozolol é famoso por promover uma secagem muscular incrível, aumento da vascularização, definição e dureza. Ele não causa grande ganho de peso, mas melhora muito a qualidade visual do corpo, além de aumentar a resistência e a força."
                },
                { 
                    name: "OXAN 10 MG", 
                    price: 170.00, 
                    benefits: "Oxandrolona na dosagem de 10mg, ideal para preservar massa magra, aumentar a força e melhorar a qualidade muscular. Excelente para ciclos de definição, cutting ou manutenção, com baixa toxidade e poucos efeitos colaterais quando bem utilizado."
                },
                { 
                    name: "OXAN 20 MG", 
                    price: 190.00, 
                    benefits: "Versão mais concentrada da Oxandrolona, com maior poder anabólico. Promove ganho de massa magra, aumento de força, dureza muscular e definição avançada. Indicada para quem busca resultados mais expressivos sem retenção de líquidos."
                },
                { 
                    name: "DIANABOL", 
                    price: 170.00, 
                    benefits: "Metandrostenolona, um dos mais clássicos e potentes orais. Promove aumento explosivo de massa muscular, força e volume em pouco tempo. Estimula a síntese proteica, a retenção de nitrogênio e a energia celular, ideal para iniciar ciclos ou quebrar platôs."
                },
                { 
                    name: "HEMOGENIN", 
                    price: 170.00, 
                    benefits: "Estimulante da produção de hemácias, aumenta o volume sanguíneo e a capacidade de transporte de oxigênio. Isso reflete em maior resistência, menos fadiga, melhor performance atlética e recuperação mais eficiente."
                }
            ],
            max: [
                { 
                    name: "ENANTATO", 
                    price: 180.00, 
                    benefits: "Testosterona Enantato de alta qualidade, ideal para ganho de massa muscular, força e disposição. Ação prolongada que mantém níveis hormonais estáveis, promovendo crescimento constante, recuperação rápida e bem-estar geral."
                },
                { 
                    name: "DURATESTON", 
                    price: 180.00, 
                    benefits: "Mistura de ésteres de testosterona com ação imediata e prolongada. Repõe níveis hormonais, aumenta libido, energia, massa magra, força e melhora a qualidade de vida e performance física."
                },
                { 
                    name: "MASTERON", 
                    price: 180.00, 
                    benefits: "Perfeito para definição muscular, reduz gordura e retenção hídrica, deixando o corpo seco, duro e vascularizado. Aumenta a densidade muscular e a dureza, com efeito antiestrogênico."
                },
                { 
                    name: "TREMBO", 
                    price: 180.00, 
                    benefits: "Trembolona de alta potência, promove ganho de massa magra, aumento da força, queima de gordura e vascularização intensa. Melhora a performance e a recuperação muscular rapidamente."
                },
                { 
                    name: "STANOZOLOL CAPS", 
                    price: 180.00, 
                    benefits: "Versão em cápsulas do Stanozolol, prática e eficaz. Promove secagem, definição, aumento da vascularização e dureza muscular. Ideal para quem quer resultados de qualidade sem injeções."
                },
                { 
                    name: "ENAN DE TREMBO", 
                    price: 180.00, 
                    benefits: "Trembolona Enantato com liberação prolongada, efeitos potentes e duradouros. Ganho de massa magra, força, definição e performance superior. Excelente para ciclos intermediários e avançados."
                },
                { 
                    name: "DECA", 
                    price: 180.00, 
                    benefits: "Nandrolona que promove ganho de massa, força, proteção articular e recuperação de lesões. Lubrifica as juntas, alivia dores e melhora a qualidade dos treinos e da vida."
                },
                { 
                    name: "OXAN 10 MG", 
                    price: 170.00, 
                    benefits: "Oxandrolona suave e eficaz, ideal para definir, preservar músculo e aumentar força. Baixa retenção hídrica, ótima para ciclos de qualidade e bem-estar."
                },
                { 
                    name: "OXAN 20 MG", 
                    price: 190.00, 
                    benefits: "Dosagem maior para resultados mais rápidos e expressivos. Aumenta massa magra, dureza, força e definição, com excelente tolerabilidade."
                },
                { 
                    name: "DIANABOL", 
                    price: 170.00, 
                    benefits: "Ganho rápido de volume e força, estimula o apetite e a energia. Clássico e eficaz para iniciar ciclos ou acelerar resultados."
                },
                { 
                    name: "STANOZOLOL", 
                    price: 180.00, 
                    benefits: "Secagem máxima, vascularização e definição muscular impressionantes. Aumenta a resistência e deixa o corpo com aparência atlética e definida."
                },
                { 
                    name: "HEMOGENIN", 
                    price: 170.00, 
                    benefits: "Aumenta glóbulos vermelhos, oxigenação muscular, resistência e performance. Ideal para melhorar capacidade física e atrasar a fadiga."
                }
            ]
        };

        let cart = [];
        let currentCategory = 'landerlan';

        function renderProducts(category) {
            const container = document.getElementById('productsContainer');
            container.innerHTML = '';
            
            products[category].forEach((product, index) => {
                const card = document.createElement('div');
                card.className = 'product-card rounded-2xl p-6 animate-fade-in';
                card.style.animationDelay = `${index * 0.1}s`;
                card.innerHTML = `
                    <div class="mb-4">
                        <h3 class="text-2xl font-bold text-white mb-2">${product.name}</h3>
                        <p class="text-4xl font-bold text-accent">R$ ${product.price.toFixed(2).replace('.', ',')}</p>
                    </div>
                    <div class="flex gap-3">
                        <button onclick="openBenefits('${product.name}', '${product.benefits}')" class="flex-1 btn-beneficios text-white py-4 rounded-xl text-xl font-bold transition">
                            BENEFÍCIOS
                        </button>
                        <div class="flex rounded-xl overflow-hidden">
                            <button onclick="removeFromCart('${product.name}')" class="w-16 h-16 bg-gray-600 hover:bg-gray-500 text-white flex items-center justify-center text-2xl font-bold btn-quantidade transition">-</button>
                            <button onclick="addToCart('${product.name}', ${product.price})" class="w-16 h-16 bg-accent hover:bg-red-700 text-white flex items-center justify-center text-2xl font-bold btn-quantidade btn-plus transition">+</button>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function openBenefits(name, text) {
            document.getElementById('benefitTitle').innerText = name;
            document.getElementById('benefitText').innerText = text;
            document.getElementById('benefitsModal').classList.remove('hidden');
            document.getElementById('benefitsModal').classList.add('flex');
        }

        function closeBenefits() {
            document.getElementById('benefitsModal').classList.add('hidden');
            document.getElementById('benefitsModal').classList.remove('flex');
        }

        function addToCart(name, price) {
            const item = cart.find(i => i.name === name && i.category === currentCategory);
            if(item) {
                item.qty++;
            } else {
                cart.push({ name, price, qty: 1, category: currentCategory.toUpperCase() });
            }
            updateCartUI();
        }

        function removeFromCart(name) {
            const item = cart.find(i => i.name === name && i.category === currentCategory);
            if(item) {
                item.qty--;
                if(item.qty <= 0) {
                    cart = cart.filter(i => !(i.name === name && i.category === currentCategory));
                }
            }
            updateCartUI();
        }

        function updateCartUI() {
            const count = cart.reduce((sum, i) => sum + i.qty, 0);
            const countEl = document.getElementById('cartCount');
            countEl.innerText = count;
            countEl.classList.add('update');
            setTimeout(() => countEl.classList.remove('update'), 500);
            
            const container = document.getElementById('cartItems');
            const totalEl = document.getElementById('cartTotal');
            
            if(cart.length === 0) {
                container.innerHTML = '<p class="text-gray-500 text-center italic">Carrinho vazio...</p>';
                totalEl.innerText = 'R$ 0,00';
            } else {
                container.innerHTML = '';
                let total = 0;
                cart.forEach(item => {
                    total += item.price * item.qty;
                    const div = document.createElement('div');
                    div.className = 'bg-gym p-3 rounded-lg transition hover:scale-105';
                    div.innerHTML = `
                        <p class="font-bold text-white mb-1">${item.name} <span class="text-accent text-sm">(${item.category})</span></p>
                        <div class="flex justify-between text-sm text-gray-400">
                            <span>Qtd: ${item.qty} | Unit: R$ ${item.price.toFixed(2).replace('.', ',')}</span>
                            <span class="text-accent font-bold">Subtotal: R$ ${(item.price * item.qty).toFixed(2).replace('.', ',')}</span>
                        </div>
                    `;
                    container.appendChild(div);
                });
                totalEl.innerText = `R$ ${total.toFixed(2).replace('.', ',')}`;
            }
        }

        function finalizeOrder() {
            if(cart.length === 0) {
                alert('Adicione produtos antes de finalizar!');
                return;
            }
            
            let totalItems = cart.reduce((sum, item) => sum + item.qty, 0);
            let totalValue = 0;
            let itemsText = '';
            
            cart.forEach(item => {
                const subt = item.price * item.qty;
                totalValue += subt;
                itemsText += `📌 ${item.qty}x ${item.name} (${item.category})\n   ➡ Unit: R$ ${item.price.toFixed(2).replace('.', ',')}\n   ➡ Subtotal: R$ ${subt.toFixed(2).replace('.', ',')}\n\n`;
            });
            
            const msg = `🛒 *PEDIDO REALIZADO COM SUCESSO!*\n\n` +
                        `${itemsText}` +
                        `📦 *Total de Itens: ${totalItems} unidades*\n` +
                        `💰 *Total Geral: R$ ${totalValue.toFixed(2).replace('.', ',')}*\n\n` +
                        `💳 *DADOS PARA PAGAMENTO VIA PIX*\n` +
                        `📱 Chave Pix: \`8596640269\`\n` +
                        `👤 Titular: Maria Edileuda Cândido Cosme\n\n` +
                        `✅ Após o pagamento, envie o comprovatante aqui!\nAgradecemos pela preferência! 💪`;
            
            const link = `https://wa.me/${phone}?text=${encodeURIComponent(msg)}`;
            window.open(link, '_blank');
        }

        // CONTROLE DAS ABAS
        document.querySelectorAll('.tab-btn').forEach(btn => {
            btn.addEventListener('click', () => {
                document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                currentCategory = btn.dataset.category;
                renderProducts(currentCategory);
            });
        });

        // CONTROLE DO CARRINHO
        document.getElementById('cartBtn').addEventListener('click', () => {
            document.getElementById('cartModal').classList.remove('hidden');
            document.getElementById('cartModal').classList.add('flex');
        });

        function closeCart() {
            document.getElementById('cartModal').classList.add('hidden');
            document.getElementById('cartModal').classList.remove('flex');
        }

        // INICIALIZAR
        renderProducts(currentCategory);
    </script>
</body>
</html>
