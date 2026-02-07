# Game_Dev_Java
import java.awt.*; import java.awt.event.*; import javax.swing.*; import java.util.Random; 
public class SnakeGame extends JFrame { 
public SnakeGame() {        
 setTitle("Snake Game");         
setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); 
setResizable(false);        
 add(new GamePanel()); 
pack();         
} 
setLocationRelativeTo(null);        
public static void main(String[] args) {         
} 
} 
 setVisible(true); 
new SnakeGame(); 
class GamePanel extends JPanel implements ActionListener, KeyListener { 
static final int SCREEN_WIDTH = 600;     static final int SCREEN_HEIGHT = 600;     static final int 
UNIT_SIZE = 20; 
static final int GAME_UNITS = 
(SCREEN_WIDTH*SCREEN_HEIGHT)/UNIT_SIZE; 
static final int DELAY = 100;     final int x[] = new int[GAME_UNITS];     final int y[] = new 
int[GAME_UNITS];     int bodyParts = 5; 
int foodX;     int foodY;     int score = 0;     char direction = 'R';     boolean running = false; 
Timer timer; 
Random random; 
GamePanel() {        
 random = new Random(); 
setPreferredSize(new Dimension(SCREEN_WIDTH, SCREEN_HEIGHT)); 
setBackground(Color.black);        
 setFocusable(true);        
} 
public void startGame() {        
 newFood();         
 addKeyListener(this);         
running = true;         
timer.start(); 
} 
public void paintComponent(Graphics g) {         
} 
public void draw(Graphics g) {         
super.paintComponent(g);        
if(running) { 
g.setColor(Color.red); 
startGame(); 
timer = new Timer(DELAY,this); 
 draw(g); 
 for(int i = 0; i < bodyParts; i++) {                 
if(i == 
g.fillOval(foodX, foodY, UNIT_SIZE, UNIT_SIZE);            
0) { 
g.setColor(Color.green); 
} else { 
g.setColor(Color.yellow); 
} 
g.fillRect(x[i], y[i], UNIT_SIZE, UNIT_SIZE); 
} 
g.setColor(Color.white); 
g.setFont(new Font("Arial", Font.BOLD, 20)); 
g.drawString("Score: " + score, 10, 30); 
} else {             
} 
} 
gameOver(g); 
public void newFood() { 
foodX = 
random.nextInt((int)(SCREEN_WIDTH/UNIT_SIZE)) * 
UNIT_SIZE; 
foodY = 
random.nextInt((int)(SCREEN_HEIGHT/UNIT_SIZE)) * UNIT_SIZE; 
} 
public void move() {         
} 
for(int i = bodyParts; i > 0; i--) {             
if(direction == 'U') y[0] -= UNIT_SIZE;         
x[i] = x[i-1];             
if(direction == 'D') y[0] += UNIT_SIZE;        
x[0] -= UNIT_SIZE;         
if(direction == 'R') x[0] += UNIT_SIZE;     } 
public void checkFood() {        
 if((x[0] == foodX) && (y[0] == foodY)) {            
y[i] = y[i-1]; 
 if(direction == 'L') 
 bodyParts++;             
score++;            
} 
} 
 newFood(); 
public void checkCollisions() {        
y[i])) {                 
} 
} 
running = false; 
 for(int i = bodyParts; i > 0; i--) {             
if(x[0] < 0 || x[0] > SCREEN_WIDTH || y[0] < 0 || y[0] 
> SCREEN_HEIGHT) { 
running = false; 
} 
if((x[0] == x[i]) && (y[0] == 
if(!running) timer.stop(); 
} 
public void gameOver(Graphics g) { 
g.setColor(Color.red); 
g.setFont(new Font("Arial", Font.BOLD, 50)); 
g.drawString("GAME OVER", 150, 250); 
g.setColor(Color.white); 
g.setFont(new Font("Arial", Font.PLAIN, 30)); 
g.drawString("Score: " + score, 220, 300); 
} 
@Override     public void actionPerformed(ActionEvent e) { 
if(running) {            
 move();             
}        
} 
 repaint(); 
checkFood();             
@Override     public void keyPressed(KeyEvent e) {        
KeyEvent.VK_UP: 
if(direction != 'D') direction = 'U';                
case KeyEvent.VK_DOWN: 
if(direction != 'U') direction = 'D';                
case KeyEvent.VK_LEFT: 
if(direction != 'R') direction = 'L';                
case KeyEvent.VK_RIGHT: 
if(direction != 'L') direction = 'R';                
} 
} 
@Override     public void keyReleased(KeyEvent e) {} 
@Override     public void keyTyped(KeyEvent e) {} 
} 
checkCollisions(); 
 switch(e.getKeyCode()) {             
 break; 
 break; 
 break; 
 break; 
case
