# Writing Training Scripts for GitHub Copilot

## Prompt 1: Creating Basic Model Training Structure
```
Intent: To help developers create training scripts for machine learning models using GitHub Copilot.

Context: You are developing a training script for a basic machine learning model. The model details are as follows:

model_type: {model_type}
dataset_description: {dataset_description}
training_objective: {training_objective}

Generate a training script structure, including:
- Data loading and basic preprocessing.
- Model definition with standard architecture.
- Simple training loop with basic evaluation.

Example:
model_type: "Neural Network for Image Classification"
dataset_description: "CIFAR-10 dataset with 60,000 32x32 color images in 10 classes"
training_objective: "Achieve >80% accuracy on test set"

Training Script Structure:
```python
import torch
import torch.nn as nn
import torch.optim as optim
import torchvision
import torchvision.transforms as transforms
from torch.utils.data import DataLoader

# Define basic preprocessing
transform = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))
])

# Load datasets
train_dataset = torchvision.datasets.CIFAR10(root='./data', train=True, 
                                             download=True, transform=transform)
test_dataset = torchvision.datasets.CIFAR10(root='./data', train=False,
                                            download=True, transform=transform)

train_loader = DataLoader(train_dataset, batch_size=64, shuffle=True)
test_loader = DataLoader(test_dataset, batch_size=64, shuffle=False)

# Define a simple CNN model
class SimpleCNN(nn.Module):
    def __init__(self):
        super(SimpleCNN, self).__init__()
        self.conv1 = nn.Conv2d(3, 32, 3, padding=1)
        self.pool = nn.MaxPool2d(2, 2)
        self.conv2 = nn.Conv2d(32, 64, 3, padding=1)
        self.fc1 = nn.Linear(64 * 8 * 8, 512)
        self.fc2 = nn.Linear(512, 10)
        self.relu = nn.ReLU()

    def forward(self, x):
        x = self.pool(self.relu(self.conv1(x)))
        x = self.pool(self.relu(self.conv2(x)))
        x = x.view(-1, 64 * 8 * 8)
        x = self.relu(self.fc1(x))
        x = self.fc2(x)
        return x

# Initialize model, loss function, and optimizer
model = SimpleCNN()
criterion = nn.CrossEntropyLoss()
optimizer = optim.SGD(model.parameters(), lr=0.01, momentum=0.9)

# Training loop
def train_model(epochs=10):
    for epoch in range(epochs):
        running_loss = 0.0
        for i, (inputs, labels) in enumerate(train_loader):
            # Zero the parameter gradients
            optimizer.zero_grad()
            
            # Forward + backward + optimize
            outputs = model(inputs)
            loss = criterion(outputs, labels)
            loss.backward()
            optimizer.step()
            
            # Print statistics
            running_loss += loss.item()
            if i % 100 == 99:
                print(f'Epoch {epoch + 1}, Batch {i + 1}, Loss: {running_loss / 100:.3f}')
                running_loss = 0.0

# Evaluation function
def evaluate_model():
    correct = 0
    total = 0
    with torch.no_grad():
        for inputs, labels in test_loader:
            outputs = model(inputs)
            _, predicted = torch.max(outputs.data, 1)
            total += labels.size(0)
            correct += (predicted == labels).sum().item()
    
    accuracy = 100 * correct / total
    print(f'Accuracy on test set: {accuracy:.2f}%')
    return accuracy

# Run training and evaluation
if __name__ == "__main__":
    train_model(epochs=10)
    evaluate_model()
```

Key points to consider:
1. Keep the architecture simple with standard components
2. Focus on basic training pipeline components: data loading, model definition, training loop, evaluation
3. Use standard libraries like PyTorch, TensorFlow or scikit-learn
4. Avoid complex custom implementations that may be difficult for Copilot to generate accurately