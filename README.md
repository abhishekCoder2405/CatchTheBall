# CatchTheBall
ball catching game 
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class CatchTheBallGame extends JPanel implements KeyListener, ActionListener {
    private int paddleX = 350;
    private int ballX = (int) (Math.random() * 700);
    private int ballY = 0;
    private int score = 0;
    private Timer timer;

    public CatchTheBallGame() {
        setFocusable(true);
        setPreferredSize(new Dimension(800, 600));
        addKeyListener(this);
        timer = new Timer(10, this);
        timer.start();
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        g.setColor(Color.BLUE);
        g.fillRect(paddleX, 550, 100, 10);
        g.setColor(Color.RED);
        g.fillOval(ballX, ballY, 20, 20);
        g.setColor(Color.BLACK);
        g.drawString("Score: " + score, 10, 10);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        ballY += 2;
        if (ballY >= 550 && ballX >= paddleX && ballX <= paddleX + 100) {
            ballY = 0;
            ballX = (int) (Math.random() * 700);
            score++;
        } else if (ballY > 600) {
            ballY = 0;
            ballX = (int) (Math.random() * 700);
        }
        repaint();
    }

    @Override
    public void keyPressed(KeyEvent e) {
        if (e.getKeyCode() == KeyEvent.VK_LEFT && paddleX > 0) {
            paddleX -= 20;
        }
        if (e.getKeyCode() == KeyEvent.VK_RIGHT && paddleX < 700) {
            paddleX += 20;
        }
        repaint();
    }

    @Override
    public void keyReleased(KeyEvent e) {}

    @Override
    public void keyTyped(KeyEvent e) {}

    public static void main(String[] args) {
        JFrame frame = new JFrame("Catch the Ball");
        CatchTheBallGame game = new CatchTheBallGame();
        frame.add(game);
        frame.pack();
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }
}
