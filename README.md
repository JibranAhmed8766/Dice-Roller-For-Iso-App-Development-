import UIKit

class ViewController: UIViewController {

    
    @IBOutlet weak var diceImageView1: UIImageView!
    @IBOutlet weak var diceImageView2: UIImageView!
    @IBOutlet weak var rollButton: UIButton!
    @IBOutlet weak var resultLabel: UILabel!
    
    
    private let diceImages = [
        UIImage(named: "dice1"),
        UIImage(named: "dice2"),
        UIImage(named: "dice3"),
        UIImage(named: "dice4"),
        UIImage(named: "dice5"),
        UIImage(named: "dice6")
    ]
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        
        rollButton.layer.cornerRadius = 12
        rollButton.backgroundColor = .systemRed
        resultLabel.text = "Press Roll to start!"
        
        
        diceImageView1.image = diceImages[0]
        diceImageView2.image = diceImages[1]
    }
    
    
    @IBAction func rollButtonTapped(_ sender: UIButton) {
        rollDice()
    }
    
    
    override func motionEnded(_ motion: UIEvent.EventSubtype, with event: UIEvent?) {
        if motion == .motionShake {
            rollDice()
        }
    }
    
    
    private func rollDice() {
        
        let randomIndex1 = Int.random(in: 0...5)
        let randomIndex2 = Int.random(in: 0...5)
        
        
        UIView.transition(with: diceImageView1, duration: 0.3, options: .transitionCrossDissolve) {
            self.diceImageView1.image = self.diceImages[randomIndex1]
        }
        
        UIView.transition(with: diceImageView2, duration: 0.3, options: .transitionCrossDissolve) {
            self.diceImageView2.image = self.diceImages[randomIndex2]
        }
        
        
        let total = (randomIndex1 + 1) + (randomIndex2 + 1)
        resultLabel.text = "You rolled: \(total)"
        
        
        let generator = UIImpactFeedbackGenerator(style: .medium)
        generator.impactOccurred()
    }
}
