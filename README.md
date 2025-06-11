```html
    body {
        font-family: 'Poppins', sans-serif;
        background-color: #f9f7f7;
    }
    
    h1, h2, h3 {
        font-family: 'Playfair Display', serif;
    }
    
    .login-bg {
        background: linear-gradient(135deg, #f8bbd0 0%, #e1bee7 100%);
    }
    
    .app-bg {
        background-color: #f9f7f7;
    }
    
    .category-card {
        transition: all 0.3s ease;
    }
    
    .category-card:hover {
        transform: translateY(-5px);
        box-shadow: 0 10px 20px rgba(0,0,0,0.1);
    }
    
    .budget-item {
        transition: background-color 0.2s ease;
    }
    
    .budget-item:hover {
        background-color: #f0e6ff;
    }
    
    .btn-primary {
        background: linear-gradient(135deg, #9c27b0 0%, #673ab7 100%);
        transition: all 0.3s ease;
    }
    
    .btn-primary:hover {
        transform: translateY(-2px);
        box-shadow: 0 5px 15px rgba(103, 58, 183, 0.4);
    }
    
    .btn-secondary {
        background: linear-gradient(135deg, #f48fb1 0%, #ce93d8 100%);
        transition: all 0.3s ease;
    }
    
    .btn-secondary:hover {
        transform: translateY(-2px);
        box-shadow: 0 5px 15px rgba(244, 143, 177, 0.4);
    }
    
    .input-field {
        transition: all 0.3s ease;
        border: 2px solid #e0e0e0;
    }
    
    .input-field:focus {
        border-color: #9c27b0;
        box-shadow: 0 0 0 3px rgba(156, 39, 176, 0.2);
    }
    
    /* Animaciones */
    @keyframes fadeIn {
        from { opacity: 0; transform: translateY(20px); }
        to { opacity: 1; transform: translateY(0); }
    }
    
    .animate-fadeIn {
        animation: fadeIn 0.5s ease forwards;
    }
    
    .delay-100 { animation-delay: 0.1s; }
    .delay-200 { animation-delay: 0.2s; }
    .delay-300 { animation-delay: 0.3s; }
    
    /* Estilos para el PDF */
    .pdf-header {
        text-align: center;
        color: #9c27b0;
        margin-bottom: 20px;
    }
    
    .pdf-section {
        margin-bottom: 15px;
    }
    
    .pdf-table {
        width: 100%;
        border-collapse: collapse;
    }
    
    .pdf-table th, .pdf-table td {
        border: 1px solid #ddd;
        padding: 8px;
    }
    
    .pdf-table th {
        background-color: #f2f2f2;
    }
    
    .pdf-footer {
        text-align: center;
        font-size: 12px;
        color: #666;
        margin-top: 30px;
    }
</style>
        <div class="mb-6 animate-fadeIn delay-100">
            <label for="username" class="block text-gray-700 font-medium mb-2">Usuario</label>
            <input type="text" id="username" class="input-field w-full px-4 py-2 rounded-lg focus:outline-none" placeholder="Ingresa tu usuario">
        </div>
        
        <div class="mb-8 animate-fadeIn delay-200">
            <label for="password" class="block text-gray-700 font-medium mb-2">Contraseña</label>
            <input type="password" id="password" class="input-field w-full px-4 py-2 rounded-lg focus:outline-none" placeholder="Ingresa tu contraseña">
            <p id="login-error" class="text-red-500 mt-2 text-sm hidden">Usuario o contraseña incorrectos</p>
        </div>
        
        <button id="login-btn" class="btn-primary w-full py-3 text-white font-medium rounded-lg animate-fadeIn delay-300">
            Iniciar Sesión
        </button>
        
        <div class="text-center mt-6 text-sm text-gray-600 animate-fadeIn delay-300">
            <p>Usuario de demostración: admin</p>
            <p>Contraseña: admin123</p>
        </div>
    </div>
</div>

<!-- Aplicación Principal -->
<div id="app" class="hidden app-bg min-h-screen">
    <!-- Barra de navegación -->
    <nav class="bg-white shadow-md">
        <div class="container mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center">
                <h1 class="text-2xl font-bold text-purple-800">Calculadora de Presupuesto</h1>
            </div>
            <div class="flex items-center space-x-4">
                <span id="user-display" class="text-gray-700 font-medium"></span>
                <button id="logout-btn" class="text-purple-600 hover:text-purple-800 font-medium">Cerrar Sesión</button>
            </div>
        </div>
    </nav>

    <!-- Contenido principal -->
    <div class="container mx-auto px-4 py-8">
        <!-- Resumen del presupuesto -->
        <div class="bg-white rounded-lg shadow-md p-6 mb-8">
            <div class="flex flex-wrap justify-between items-center">
                <div>
                    <h2 class="text-2xl font-bold text-gray-800">Resumen del Presupuesto</h2>
                    <p class="text-gray-600 mt-1">Gestiona y controla tus gastos para la boda</p>
                </div>
                <div class="mt-4 sm:mt-0">
                    <button id="new-budget-btn" class="btn-primary px-6 py-2 text-white font-medium rounded-lg mr-2">
                        Nuevo Presupuesto
                    </button>
                    <button id="save-budget-btn" class="btn-secondary px-6 py-2 text-white font-medium rounded-lg">
                        Guardar Presupuesto
                    </button>
                </div>
            </div>
            
            <div class="mt-6 grid grid-cols-1 md:grid-cols-3 gap-6">
                <div class="bg-purple-50 rounded-lg p-4 border-l-4 border-purple-500">
                    <h3 class="text-lg font-semibold text-purple-800">Presupuesto Total</h3>
                    <div class="flex items-end mt-2">
                        <span id="total-budget" class="text-3xl font-bold text-purple-900">$0</span>
                        <input type="number" id="budget-input" class="input-field ml-3 px-3 py-1 w-32 rounded-lg text-gray-700" placeholder="Definir">
                    </div>
                </div>
                
                <div class="bg-pink-50 rounded-lg p-4 border-l-4 border-pink-500">
                    <h3 class="text-lg font-semibold text-pink-800">Gastos Actuales</h3>
                    <p id="current-expenses" class="text-3xl font-bold text-pink-900 mt-2">$0</p>
                </div>
                
                <div class="bg-green-50 rounded-lg p-4 border-l-4 border-green-500">
                    <h3 class="text-lg font-semibold text-green-800">Saldo Restante</h3>
                    <p id="remaining-budget" class="text-3xl font-bold text-green-900 mt-2">$0</p>
                </div>
            </div>
        </div>

        <!-- Categorías de gastos -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-8">
            <div class="category-card bg-white rounded-lg shadow-md p-6 cursor-pointer" data-category="venue">
                <div class="flex items-center justify-between">
                    <h3 class="text-xl font-bold text-gray-800">Lugar y Catering</h3>
                    <span class="category-amount text-lg font-semibold text-purple-700">$0</span>
                </div>
                <p class="text-gray-600 mt-2">Salón, comida, bebidas, pastel</p>
            </div>
            
            <div class="category-card bg-white rounded-lg shadow-md p-6 cursor-pointer" data-category="attire">
                <div class="flex items-center justify-between">
                    <h3 class="text-xl font-bold text-gray-800">Vestimenta</h3>
                    <span class="category-amount text-lg font-semibold text-purple-700">$0</span>
                </div>
                <p class="text-gray-600 mt-2">Vestido, traje, accesorios</p>
            </div>
            
            <div class="category-card bg-white rounded-lg shadow-md p-6 cursor-pointer" data-category="photography">
                <div class="flex items-center justify-between">
                    <h3 class="text-xl font-bold text-gray-800">Fotografía y Video</h3>
                    <span class="category-amount text-lg font-semibold text-purple-700">$0</span>
                </div>
                <p class="text-gray-600 mt-2">Fotógrafo, videógrafo, álbum</p>
            </div>
            
            <div class="category-card bg-white rounded-lg shadow-md p-6 cursor-pointer" data-category="decoration">
                <div class="flex items-center justify-between">
                    <h3 class="text-xl font-bold text-gray-800">Decoración</h3>
                    <span class="category-amount text-lg font-semibold text-purple-700">$0</span>
                </div>
                <p class="text-gray-600 mt-2">Flores, centros de mesa, iluminación</p>
            </div>
            
            <div class="category-card bg-white rounded-lg shadow-md p-6 cursor-pointer" data-category="music">
                <div class="flex items-center justify-between">
                    <h3 class="text-xl font-bold text-gray-800">Música y Entretenimiento</h3>
                    <span class="category-amount text-lg font-semibold text-purple-700">$0</span>
                </div>
                <p class="text-gray-600 mt-2">DJ, banda, animación</p>
            </div>
            
            <div class="category-card bg-white rounded-lg shadow-md p-6 cursor-pointer" data-category="others">
                <div class="flex items-center justify-between">
                    <h3 class="text-xl font-bold text-gray-800">Otros Gastos</h3>
                    <span class="category-amount text-lg font-semibold text-purple-700">$0</span>
                </div>
                <p class="text-gray-600 mt-2">Invitaciones, transporte, regalos</p>
            </div>
        </div>

        <!-- Lista de presupuestos guardados -->
        <div class="bg-white rounded-lg shadow-md p-6">
            <h2 class="text-2xl font-bold text-gray-800 mb-4">Presupuestos Guardados</h2>
            <div id="saved-budgets-list" class="space-y-3">
                <!-- Los presupuestos guardados se mostrarán aquí -->
                <p id="no-budgets-message" class="text-gray-500 italic">No hay presupuestos guardados</p>
            </div>
        </div>
    </div>

    <!-- Modal para detalles de categoría -->
    <div id="category-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-lg shadow-xl p-6 max-w-2xl w-full max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-6">
                <h2 id="modal-title" class="text-2xl font-bold text-purple-800">Detalles de Categoría</h2>
                <button id="close-modal-btn" class="text-gray-500 hover:text-gray-700 text-xl font-bold">&times;</button>
            </div>
            
            <div id="category-items" class="space-y-4 mb-6">
                <!-- Los items de la categoría se mostrarán aquí -->
            </div>
            
            <div class="border-t border-gray-200 pt-4">
                <div class="flex items-center mb-4">
                    <input type="text" id="new-item-name" class="input-field flex-grow px-4 py-2 rounded-lg mr-2" placeholder="Nombre del item">
                    <input type="number" id="new-item-amount" class="input-field w-32 px-4 py-2 rounded-lg" placeholder="Monto">
                </div>
                <button id="add-item-btn" class="btn-primary px-6 py-2 text-white font-medium rounded-lg">
                    Agregar Item
                </button>
            </div>
            
            <div class="flex justify-between items-center mt-6 pt-4 border-t border-gray-200">
                <div>
                    <p class="text-gray-700">Total de la categoría:</p>
                    <p id="modal-category-total" class="text-2xl font-bold text-purple-900">$0</p>
                </div>
                <button id="save-category-btn" class="btn-secondary px-6 py-2 text-white font-medium rounded-lg">
                    Guardar Cambios
                </button>
            </div>
        </div>
    </div>

    <!-- Modal para guardar presupuesto -->
    <div id="save-budget-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-lg shadow-xl p-6 max-w-md w-full">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-2xl font-bold text-purple-800">Guardar Presupuesto</h2>
                <button id="close-save-modal-btn" class="text-gray-500 hover:text-gray-700 text-xl font-bold">&times;</button>
            </div>
            
            <div class="mb-6">
                <label for="budget-name" class="block text-gray-700 font-medium mb-2">Nombre del Presupuesto</label>
                <input type="text" id="budget-name" class="input-field w-full px-4 py-2 rounded-lg" placeholder="Ej: Presupuesto Inicial">
            </div>
            
            <div class="mb-6">
                <label for="budget-description" class="block text-gray-700 font-medium mb-2">Descripción (opcional)</label>
                <textarea id="budget-description" class="input-field w-full px-4 py-2 rounded-lg" rows="3" placeholder="Añade una descripción para este presupuesto"></textarea>
            </div>
            
            <div class="flex justify-end">
                <button id="confirm-save-budget-btn" class="btn-primary px-6 py-2 text-white font-medium rounded-lg">
                    Guardar
                </button>
            </div>
        </div>
    </div>

    <!-- Modal para ver detalles del presupuesto guardado -->
    <div id="view-budget-modal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-lg shadow-xl p-6 max-w-4xl w-full max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-6">
                <h2 id="view-budget-title" class="text-2xl font-bold text-purple-800">Detalles del Presupuesto</h2>
                <button id="close-view-modal-btn" class="text-gray-500 hover:text-gray-700 text-xl font-bold">&times;</button>
            </div>
            
            <div id="view-budget-content" class="space-y-6">
                <!-- El contenido del presupuesto se mostrará aquí -->
            </div>
            
            <div class="flex justify-between items-center mt-8 pt-4 border-t border-gray-200">
                <button id="delete-budget-btn" class="px-6 py-2 bg-red-500 hover:bg-red-600 text-white font-medium rounded-lg">
                    Eliminar
                </button>
                <div class="flex space-x-3">
                    <button id="load-budget-btn" class="btn-secondary px-6 py-2 text-white font-medium rounded-lg">
                        Cargar Presupuesto
                    </button>
                    <button id="export-pdf-btn" class="btn-primary px-6 py-2 text-white font-medium rounded-lg">
                        Exportar PDF
                    </button>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
    document.addEventListener('DOMContentLoaded', function() {
        // Variables globales
        let currentBudget = {
            total: 0,
            categories: {
                venue: { name: 'Lugar y Catering', items: [] },
                attire: { name: 'Vestimenta', items: [] },
                photography: { name: 'Fotografía y Video', items: [] },
                decoration: { name: 'Decoración', items: [] },
                music: { name: 'Música y Entretenimiento', items: [] },
                others: { name: 'Otros Gastos', items: [] }
            }
        };
        
        let currentCategory = '';
        let savedBudgets = JSON.parse(localStorage.getItem('weddingBudgets')) || [];
        let currentBudgetIndex = -1;
        
        // Elementos DOM
        const loginScreen = document.getElementById('login-screen');
        const app = document.getElementById('app');
        const loginBtn = document.getElementById('login-btn');
        const logoutBtn = document.getElementById('logout-btn');
        const userDisplay = document.getElementById('user-display');
        const loginError = document.getElementById('login-error');
        
        const totalBudgetDisplay = document.getElementById('total-budget');
        const budgetInput = document.getElementById('budget-input');
        const currentExpensesDisplay = document.getElementById('current-expenses');
        const remainingBudgetDisplay = document.getElementById('remaining-budget');
        
        const categoryCards = document.querySelectorAll('.category-card');
        const categoryModal = document.getElementById('category-modal');
        const modalTitle = document.getElementById('modal-title');
        const categoryItems = document.getElementById('category-items');
        const closeModalBtn = document.getElementById('close-modal-btn');
        const newItemName = document.getElementById('new-item-name');
        const newItemAmount = document.getElementById('new-item-amount');
        const addItemBtn = document.getElementById('add-item-btn');
        const modalCategoryTotal = document.getElementById('modal-category-total');
        const saveCategoryBtn = document.getElementById('save-category-btn');
        
        const newBudgetBtn = document.getElementById('new-budget-btn');
        const saveBudgetBtn = document.getElementById('save-budget-btn');
        const saveBudgetModal = document.getElementById('save-budget-modal');
        const closeSaveModalBtn = document.getElementById('close-save-modal-btn');
        const budgetName = document.getElementById('budget-name');
        const budgetDescription = document.getElementById('budget-description');
        const confirmSaveBudgetBtn = document.getElementById('confirm-save-budget-btn');
        
        const savedBudgetsList = document.getElementById('saved-budgets-list');
        const noBudgetsMessage = document.getElementById('no-budgets-message');
        
        const viewBudgetModal = document.getElementById('view-budget-modal');
        const viewBudgetTitle = document.getElementById('view-budget-title');
        const viewBudgetContent = document.getElementById('view-budget-content');
        const closeViewModalBtn = document.getElementById('close-view-modal-btn');
        const deleteBudgetBtn = document.getElementById('delete-budget-btn');
        const loadBudgetBtn = document.getElementById('load-budget-btn');
        const exportPdfBtn = document.getElementById('export-pdf-btn');
        
        // Funciones de autenticación
        loginBtn.addEventListener('click', function() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            if (username === 'admin' && password === 'admin123') {
                loginScreen.classList.add('hidden');
                app.classList.remove('hidden');
                userDisplay.textContent = `¡Hola, ${username}!`;
                loginError.classList.add('hidden');
            } else {
                loginError.classList.remove('hidden');
            }
        });
        
        logoutBtn.addEventListener('click', function() {
            app.classList.add('hidden');
            loginScreen.classList.remove('hidden');
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
        });
        
        // Funciones de presupuesto
        budgetInput.addEventListener('change', function() {
            const budgetValue = parseFloat(budgetInput.value) || 0;
            currentBudget.total = budgetValue;
            updateBudgetDisplay();
        });
        
        function updateBudgetDisplay() {
            // Actualizar el presupuesto total
            totalBudgetDisplay.textContent = formatCurrency(currentBudget.total);
            
            // Calcular y actualizar los gastos actuales
            let totalExpenses = 0;
            for (const category in currentBudget.categories) {
                let categoryTotal = 0;
                currentBudget.categories[category].items.forEach(item => {
                    categoryTotal += item.amount;
                });
                totalExpenses += categoryTotal;
                
                // Actualizar el monto mostrado en la tarjeta de categoría
                const categoryCard = document.querySelector(`.category-card[data-category="${category}"]`);
                if (categoryCard) {
                    const amountElement = categoryCard.querySelector('.category-amount');
                    amountElement.textContent = formatCurrency(categoryTotal);
                }
            }
            
            currentExpensesDisplay.textContent = formatCurrency(totalExpenses);
            
            // Calcular y actualizar el saldo restante
            const remaining = currentBudget.total - totalExpenses;
            remainingBudgetDisplay.textContent = formatCurrency(remaining);
            
            // Cambiar el color del saldo restante según su valor
            if (remaining < 0) {
                remainingBudgetDisplay.classList.remove('text-green-900');
                remainingBudgetDisplay.classList.add('text-red-600');
            } else {
                remainingBudgetDisplay.classList.remove('text-red-600');
                remainingBudgetDisplay.classList.add('text-green-900');
            }
        }
        
        // Funciones de categorías
        categoryCards.forEach(card => {
            card.addEventListener('click', function() {
                const category = this.getAttribute('data-category');
                openCategoryModal(category);
            });
        });
        
        function openCategoryModal(category) {
            currentCategory = category;
            modalTitle.textContent = currentBudget.categories[category].name;
            
            // Limpiar y llenar los items de la categoría
            categoryItems.innerHTML = '';
            let categoryTotal = 0;
            
            currentBudget.categories[category].items.forEach((item, index) => {
                categoryTotal += item.amount;
                addItemToModal(item.name, item.amount, index);
            });
            
            modalCategoryTotal.textContent = formatCurrency(categoryTotal);
            categoryModal.classList.remove('hidden');
            
            // Limpiar los campos de nuevo item
            newItemName.value = '';
            newItemAmount.value = '';
        }
        
        function addItemToModal(name, amount, index) {
            const itemElement = document.createElement('div');
            itemElement.className = 'budget-item flex justify-between items-center p-3 bg-gray-50 rounded-lg';
            itemElement.innerHTML = `
                <span class="font-medium text-gray-800">${name}</span>
                <div class="flex items-center">
                    <span class="font-semibold text-purple-700 mr-3">${formatCurrency(amount)}</span>
                    <button class="delete-item-btn text-red-500 hover:text-red-700" data-index="${index}">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                            <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
                        </svg>
                    </button>
                </div>
            `;
            
            categoryItems.appendChild(itemElement);
            
            // Agregar evento para eliminar item
            const deleteBtn = itemElement.querySelector('.delete-item-btn');
            deleteBtn.addEventListener('click', function() {
                const itemIndex = parseInt(this.getAttribute('data-index'));
                deleteItem(itemIndex);
            });
        }
        
        function deleteItem(index) {
            currentBudget.categories[currentCategory].items.splice(index, 1);
            openCategoryModal(currentCategory); // Recargar el modal
        }
        
        addItemBtn.addEventListener('click', function() {
            const name = newItemName.value.trim();
            const amount = parseFloat(newItemAmount.value) || 0;
            
            if (name && amount > 0) {
                currentBudget.categories[currentCategory].items.push({ name, amount });
                openCategoryModal(currentCategory); // Recargar el modal
            }
        });
        
        closeModalBtn.addEventListener('click', function() {
            categoryModal.classList.add('hidden');
        });
        
        saveCategoryBtn.addEventListener('click', function() {
            categoryModal.classList.add('hidden');
            updateBudgetDisplay();
        });
        
        // Funciones para guardar y cargar presupuestos
        newBudgetBtn.addEventListener('click', function() {
            if (confirm('¿Estás seguro de crear un nuevo presupuesto? Se perderán los datos no guardados.')) {
                currentBudget = {
                    total: 0,
                    categories: {
                        venue: { name: 'Lugar y Catering', items: [] },
                        attire: { name: 'Vestimenta', items: [] },
                        photography: { name: 'Fotografía y Video', items: [] },
                        decoration: { name: 'Decoración', items: [] },
                        music: { name: 'Música y Entretenimiento', items: [] },
                        others: { name: 'Otros Gastos', items: [] }
                    }
                };
                budgetInput.value = '';
                currentBudgetIndex = -1;
                updateBudgetDisplay();
            }
        });
        
        saveBudgetBtn.addEventListener('click', function() {
            budgetName.value = '';
            budgetDescription.value = '';
            saveBudgetModal.classList.remove('hidden');
        });
        
        closeSaveModalBtn.addEventListener('click', function() {
            saveBudgetModal.classList.add('hidden');
        });
        
        confirmSaveBudgetBtn.addEventListener('click', function() {
            const name = budgetName.value.trim();
            const description = budgetDescription.value.trim();
            const date = new Date().toLocaleDateString();
            
            if (name) {
                const budgetToSave = {
                    name,
                    description,
                    date,
                    budget: JSON.parse(JSON.stringify(currentBudget)) // Copia profunda
                };
                
                if (currentBudgetIndex >= 0) {
                    // Actualizar presupuesto existente
                    savedBudgets[currentBudgetIndex] = budgetToSave;
                } else {
                    // Guardar nuevo presupuesto
                    savedBudgets.push(budgetToSave);
                    currentBudgetIndex = savedBudgets.length - 1;
                }
                
                localStorage.setItem('weddingBudgets', JSON.stringify(savedBudgets));
                saveBudgetModal.classList.add('hidden');
                updateSavedBudgetsList();
            }
        });
        
        function updateSavedBudgetsList() {
            savedBudgetsList.innerHTML = '';
            
            if (savedBudgets.length === 0) {
                noBudgetsMessage.classList.remove('hidden');
            } else {
                noBudgetsMessage.classList.add('hidden');
                
                savedBudgets.forEach((budget, index) => {
                    // Calcular el total de gastos
                    let totalExpenses = 0;
                    for (const category in budget.budget.categories) {
                        budget.budget.categories[category].items.forEach(item => {
                            totalExpenses += item.amount;
                        });
                    }
                    
                    const budgetElement = document.createElement('div');
                    budgetElement.className = 'budget-item flex justify-between items-center p-4 bg-gray-50 rounded-lg hover:bg-gray-100 cursor-pointer';
                    budgetElement.innerHTML = `
                        <div>
                            <h3 class="font-semibold text-gray-800">${budget.name}</h3>
                            <p class="text-sm text-gray-600">Creado: ${budget.date}</p>
                        </div>
                        <div class="text-right">
                            <p class="font-semibold text-purple-700">${formatCurrency(budget.budget.total)}</p>
                            <p class="text-sm text-gray-600">Gastos: ${formatCurrency(totalExpenses)}</p>
                        </div>
                    `;
                    
                    budgetElement.addEventListener('click', function() {
                        openBudgetDetails(index);
                    });
                    
                    savedBudgetsList.appendChild(budgetElement);
                });
            }
        }
        
        function openBudgetDetails(index) {
            const budget = savedBudgets[index];
            viewBudgetTitle.textContent = budget.name;
            
            // Limpiar y llenar el contenido
            viewBudgetContent.innerHTML = '';
            
            // Información general
            const infoSection = document.createElement('div');
            infoSection.className = 'mb-6';
            infoSection.innerHTML = `
                <p class="text-gray-600"><strong>Fecha:</strong> ${budget.date}</p>
                ${budget.description ? `<p class="text-gray-600 mt-2"><strong>Descripción:</strong> ${budget.description}</p>` : ''}
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-4">
                    <div class="bg-purple-50 p-3 rounded-lg">
                        <p class="text-sm text-purple-800">Presupuesto Total</p>
                        <p class="text-xl font-bold text-purple-900">${formatCurrency(budget.budget.total)}</p>
                    </div>
                    <div class="bg-pink-50 p-3 rounded-lg">
                        <p class="text-sm text-pink-800">Gastos Totales</p>
                        <p class="text-xl font-bold text-pink-900" id="view-total-expenses">Calculando...</p>
                    </div>
                    <div class="bg-green-50 p-3 rounded-lg">
                        <p class="text-sm text-green-800">Saldo Restante</p>
                        <p class="text-xl font-bold" id="view-remaining">Calculando...</p>
                    </div>
                </div>
            `;
            viewBudgetContent.appendChild(infoSection);
            
            // Detalles por categoría
            let totalExpenses = 0;
            
            for (const categoryKey in budget.budget.categories) {
                const category = budget.budget.categories[categoryKey];
                let categoryTotal = 0;
                
                // Calcular el total de la categoría
                category.items.forEach(item => {
                    categoryTotal += item.amount;
                });
                
                totalExpenses += categoryTotal;
                
                // Solo mostrar categorías con items
                if (category.items.length > 0) {
                    const categorySection = document.createElement('div');
                    categorySection.className = 'mb-6';
                    
                    let itemsHTML = '';
                    category.items.forEach(item => {
                        itemsHTML += `
                            <div class="flex justify-between py-2 border-b border-gray-100">
                                <span>${item.name}</span>
                                <span class="font-medium">${formatCurrency(item.amount)}</span>
                            </div>
                        `;
                    });
                    
                    categorySection.innerHTML = `
                        <div class="flex justify-between items-center mb-2">
                            <h3 class="text-lg font-semibold text-gray-800">${category.name}</h3>
                            <span class="font-bold text-purple-700">${formatCurrency(categoryTotal)}</span>
                        </div>
                        <div class="bg-gray-50 p-3 rounded-lg">
                            ${itemsHTML}
                        </div>
                    `;
                    
                    viewBudgetContent.appendChild(categorySection);
                }
            }
            
            // Actualizar los totales
            const viewTotalExpenses = document.getElementById('view-total-expenses');
            const viewRemaining = document.getElementById('view-remaining');
            const remaining = budget.budget.total - totalExpenses;
            
            viewTotalExpenses.textContent = formatCurrency(totalExpenses);
            viewRemaining.textContent = formatCurrency(remaining);
            
            if (remaining < 0) {
                viewRemaining.classList.add('text-red-600');
                viewRemaining.classList.remove('text-green-900');
            } else {
                viewRemaining.classList.add('text-green-900');
                viewRemaining.classList.remove('text-red-600');
            }
            
            // Configurar botones
            deleteBudgetBtn.setAttribute('data-index', index);
            loadBudgetBtn.setAttribute('data-index', index);
            exportPdfBtn.setAttribute('data-index', index);
            
            viewBudgetModal.classList.remove('hidden');
        }
        
        closeViewModalBtn.addEventListener('click', function() {
            viewBudgetModal.classList.add('hidden');
        });
        
        deleteBudgetBtn.addEventListener('click', function() {
            const index = parseInt(this.getAttribute('data-index'));
            
            if (confirm('¿Estás seguro de eliminar este presupuesto? Esta acción no se puede deshacer.')) {
                savedBudgets.splice(index, 1);
                localStorage.setItem('weddingBudgets', JSON.stringify(savedBudgets));
                
                if (currentBudgetIndex === index) {
                    currentBudgetIndex = -1;
                } else if (currentBudgetIndex > index) {
                    currentBudgetIndex--;
                }
                
                viewBudgetModal.classList.add('hidden');
                updateSavedBudgetsList();
            }
        });
        
        loadBudgetBtn.addEventListener('click', function() {
            const index = parseInt(this.getAttribute('data-index'));
            
            if (confirm('¿Estás seguro de cargar este presupuesto? Se perderán los cambios no guardados en el presupuesto actual.')) {
                currentBudget = JSON.parse(JSON.stringify(savedBudgets[index].budget)); // Copia profunda
                currentBudgetIndex = index;
                
                budgetInput.value = currentBudget.total;
                updateBudgetDisplay();
                viewBudgetModal.classList.add('hidden');
            }
        });
        
        exportPdfBtn.addEventListener('click', function() {
            const index = parseInt(this.getAttribute('data-index'));
            const budget = savedBudgets[index];
            
            // Calcular totales
            let totalExpenses = 0;
            for (const categoryKey in budget.budget.categories) {
                const category = budget.budget.categories[categoryKey];
                category.items.forEach(item => {
                    totalExpenses += item.amount;
                });
            }
            const remaining = budget.budget.total - totalExpenses;
            
            // Generar PDF
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            
            // Título
            doc.setFontSize(22);
            doc.setTextColor(128, 0, 128); // Púrpura
            doc.text('Presupuesto de Boda', 105, 20, { align: 'center' });
            
            // Información general
            doc.setFontSize(14);
            doc.setTextColor(0, 0, 0);
            doc.text(`Nombre: ${budget.name}`, 20, 35);
            doc.text(`Fecha: ${budget.date}`, 20, 42);
            
            if (budget.description) {
                doc.text('Descripción:', 20, 49);
                doc.setFontSize(12);
                doc.text(budget.description, 20, 56);
            }
            
            // Resumen financiero
            let yPos = budget.description ? 70 : 56;
            
            doc.setFontSize(14);
            doc.text('Resumen Financiero', 20, yPos);
            yPos += 7;
            
            doc.setFontSize(12);
            doc.text(`Presupuesto Total: ${formatCurrency(budget.budget.total)}`, 25, yPos);
            yPos += 7;
            doc.text(`Gastos Totales: ${formatCurrency(totalExpenses)}`, 25, yPos);
            yPos += 7;
            doc.text(`Saldo Restante: ${formatCurrency(remaining)}`, 25, yPos);
            yPos += 15;
            
            // Detalles por categoría
            doc.setFontSize(14);
            doc.text('Detalles por Categoría', 20, yPos);
            yPos += 10;
            
            for (const categoryKey in budget.budget.categories) {
                const category = budget.budget.categories[categoryKey];
                
                // Solo mostrar categorías con items
                if (category.items.length > 0) {
                    let categoryTotal = 0;
                    category.items.forEach(item => {
                        categoryTotal += item.amount;
                    });
                    
                    // Verificar si necesitamos una nueva página
                    if (yPos > 250) {
                        doc.addPage();
                        yPos = 20;
                    }
                    
                    doc.setFontSize(13);
                    doc.setTextColor(128, 0, 128); // Púrpura
                    doc.text(`${category.name} - ${formatCurrency(categoryTotal)}`, 20, yPos);
                    yPos += 7;
                    
                    doc.setFontSize(11);
                    doc.setTextColor(0, 0, 0);
                    
                    category.items.forEach(item => {
                        // Verificar si necesitamos una nueva página
                        if (yPos > 270) {
                            doc.addPage();
                            yPos = 20;
                        }
                        
                        doc.text(`${item.name}: ${formatCurrency(item.amount)}`, 25, yPos);
                        yPos += 6;
                    });
                    
                    yPos += 5;
                }
            }
            
            // Pie de página
            const pageCount = doc.internal.getNumberOfPages();
            for (let i = 1; i <= pageCount; i++) {
                doc.setPage(i);
                doc.setFontSize(10);
                doc.setTextColor(150, 150, 150);
                doc.text(`Página ${i} de ${pageCount}`, 105, 290, { align: 'center' });
            }
            
            // Guardar PDF
            doc.save(`Presupuesto_${budget.name.replace(/\s+/g, '_')}.pdf`);
        });
        
        // Funciones de utilidad
        function formatCurrency(amount) {
            return '$' + amount.toLocaleString('es-ES', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
        }
        
        // Inicialización
        updateBudgetDisplay();
        updateSavedBudgetsList();
    });
</script>
