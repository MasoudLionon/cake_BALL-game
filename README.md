# cake_BALL-game
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimpleGame extends JFrame implements ActionListener {

    private static final int WIDTH = 500;
    private static final int HEIGHT = 500;

    private int ballX = 50;
    private int ballY = 50;
    private int ballSpeedX = 2;
    private int ballSpeedY = 3;

    public SimpleGame() {
        setTitle("Simple Game");
        setSize(WIDTH, HEIGHT);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        Timer timer = new Timer(10, this);
        timer.start();

        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        moveBall();
        repaint();
    }

    private void moveBall() {
        ballX += ballSpeedX;
        ballY += ballSpeedY;

        // Check for collisions with the walls
        if (ballX < 0 || ballX > WIDTH - 20) {
            ballSpeedX = -ballSpeedX;
        }

        if (ballY < 0 || ballY > HEIGHT - 20) {
            ballSpeedY = -ballSpeedY;
        }
    }

    @Override
    public void paint(Graphics g) {
        super.paint(g);
        drawBall(g);
    }

    private void drawBall(Graphics g) {
        g.setColor(Color.BLUE);
        g.fillOval(ballX, ballY, 20, 20);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new SimpleGame();
            }
        });
    }
}
