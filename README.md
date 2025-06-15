# roblox-ai-qui


--[[ 
🧠 AI Science QuizBot (All-in-One Script)
By: [Your Name]
A single-file science quiz game hosted by a simulated AI in Roblox. Paste this into a LocalScript under StarterGui.
--]]

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "ScienceQuizBot"

-- UI Setup
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0.65, 0, 0.6, 0)
frame.Position = UDim2.new(0.175, 0, 0.2, 0)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
frame.BorderSizePixel = 0

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0.15, 0)
title.Text = "🤖 AI Science QuizBot"
title.TextScaled = true
title.BackgroundTransparency = 1
title.TextColor3 = Color3.fromRGB(0, 255, 200)

local questionLabel = Instance.new("TextLabel", frame)
questionLabel.Size = UDim2.new(0.9, 0, 0.2, 0)
questionLabel.Position = UDim2.new(0.05, 0, 0.2, 0)
questionLabel.TextScaled = true
questionLabel.TextWrapped = true
questionLabel.BackgroundTransparency = 1
questionLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
questionLabel.Text = ""

local inputBox = Instance.new("TextBox", frame)
inputBox.Size = UDim2.new(0.7, 0, 0.15, 0)
inputBox.Position = UDim2.new(0.05, 0, 0.5, 0)
inputBox.PlaceholderText = "Type your answer here..."
inputBox.Text = ""
inputBox.TextScaled = true
inputBox.ClearTextOnFocus = false
inputBox.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
inputBox.TextColor3 = Color3.fromRGB(0, 0, 0)

local submitBtn = Instance.new("TextButton", frame)
submitBtn.Size = UDim2.new(0.2, 0, 0.15, 0)
submitBtn.Position = UDim2.new(0.75, 0, 0.5, 0)
submitBtn.Text = "Submit"
submitBtn.TextScaled = true
submitBtn.BackgroundColor3 = Color3.fromRGB(0, 200, 255)

local feedbackLabel = Instance.new("TextLabel", frame)
feedbackLabel.Size = UDim2.new(0.9, 0, 0.15, 0)
feedbackLabel.Position = UDim2.new(0.05, 0, 0.7, 0)
feedbackLabel.TextScaled = true
feedbackLabel.TextWrapped = true
feedbackLabel.BackgroundTransparency = 1
feedbackLabel.TextColor3 = Color3.fromRGB(255, 255, 200)
feedbackLabel.Text = ""

-- Questions & Answers
local quizData = {
	{ question = "What planet is known as the Red Planet?", answer = "mars" },
	{ question = "What gas do plants absorb from the atmosphere?", answer = "carbon dioxide" },
	{ question = "What force keeps us on the ground?", answer = "gravity" },
	{ question = "How many legs does an insect have?", answer = "6" },
	{ question = "What is H2O commonly known as?", answer = "water" },
	{ question = "What is the powerhouse of the cell?", answer = "mitochondria" },
}

local currentQuestion = 1

local function askQuestion()
	local q = quizData[currentQuestion]
	if q then
		questionLabel.Text = "Q" .. currentQuestion .. ": " .. q.question
	else
		questionLabel.Text = "🎉 You finished all questions!"
		feedbackLabel.Text = "Thanks for playing! Reload to try again."
		inputBox.Visible = false
		submitBtn.Visible = false
	end
end

submitBtn.MouseButton1Click:Connect(function()
	local userAnswer = string.lower(inputBox.Text)
	local correct = string.lower(quizData[currentQuestion].answer)

	if userAnswer == correct then
		feedbackLabel.Text = "✅ Correct! Nice job."
	else
		feedbackLabel.Text = "❌ Oops! The correct answer was: " .. correct
	end

	currentQuestion += 1
	inputBox.Text = ""
	wait(1.5)
	feedbackLabel.Text = ""
	askQuestion()
end)

-- Start quiz
askQuestion()
