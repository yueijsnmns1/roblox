-- Script de ESP no Roblox Studio

-- Função para criar a caixa de ESP em torno de um jogador
local function criarESP(player)
    -- Verifica se o personagem do jogador existe
    local character = player.Character
    if not character then return end
    
    -- Cria um BillboardGui para exibir a caixa do ESP
    local espGui = Instance.new("BillboardGui")
    espGui.Adornee = character:WaitForChild("Head")  -- Coloca o ESP na cabeça do jogador
    espGui.Size = UDim2.new(0, 100, 0, 100)  -- Tamanho da caixa
    espGui.StudsOffset = Vector3.new(0, 2, 0)  -- Distância do jogador (altura)
    espGui.Parent = character  -- Coloca a GUI no personagem
    
    -- Cria uma Frame dentro do BillboardGui para simular a caixa
    local espBox = Instance.new("Frame")
    espBox.Size = UDim2.new(1, 0, 1, 0)  -- Preenche todo o espaço do BillboardGui
    espBox.BackgroundColor3 = Color3.fromRGB(255, 0, 0)  -- Cor da caixa (vermelha)
    espBox.BackgroundTransparency = 0.5  -- Transparência da caixa
    espBox.BorderSizePixel = 2  -- Tamanho da borda da caixa
    espBox.Parent = espGui  -- Coloca a caixa dentro do BillboardGui
end

-- Função para remover o ESP quando o jogador sai
local function removerESP(player)
    -- Verifica se o personagem do jogador existe
    local character = player.Character
    if not character then return end
    
    -- Encontra o BillboardGui e remove
    local espGui = character:FindFirstChildOfClass("BillboardGui")
    if espGui then
        espGui:Destroy()  -- Remove a caixa de ESP
    end
end

-- Conectar as funções aos eventos do jogo
game.Players.PlayerAdded:Connect(function(player)
    -- Quando o jogador entrar no jogo, cria o ESP
    player.CharacterAdded:Connect(function()
        criarESP(player)
    end)
end)

game.Players.PlayerRemoving:Connect(function(player)
    -- Quando o jogador sair do jogo, remove o ESP
    removerESP(player)
end)
