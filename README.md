# 301-2-Code

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.canvas.Canvas;
import javafx.scene.control.Menu;
import javafx.scene.control.MenuBar;
import javafx.scene.layout.BorderPane;
import javafx.stage.Stage;

public class BasicDrawingApp extends Application {

    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        Canvas canvas = new Canvas(800, 600);
        MenuBar menuBar = new MenuBar();

        // File Menu
        Menu fileMenu = new Menu("File");
        menuBar.getMenus().add(fileMenu);

        // Edit Menu
        Menu editMenu = new Menu("Edit");
        menuBar.getMenus().add(editMenu);

        // Tools Menu
        Menu toolsMenu = new Menu("Tools");
        menuBar.getMenus().add(toolsMenu);

        BorderPane root = new BorderPane();
        root.setTop(menuBar);
        root.setCenter(canvas);

        Scene scene = new Scene(root, 800, 600);
        primaryStage.setScene(scene);
        primaryStage.setTitle("Basic Drawing App");
        primaryStage.show();
    }
}

Prompt 2 

import javafx.scene.canvas.GraphicsContext;
import javafx.scene.input.MouseEvent;

// Inside the BasicDrawingApp class
@Override
public void start(Stage primaryStage) {
    // ... existing code ...
    GraphicsContext gc = canvas.getGraphicsContext2D();

    canvas.setOnMousePressed(e -> gc.beginPath());
    canvas.setOnMouseDragged(e -> {
        gc.lineTo(e.getX(), e.getY());
        gc.stroke();
    });
    canvas.setOnMouseReleased(e -> gc.closePath());
}

Prompt 3

import javafx.scene.image.WritableImage;
import javafx.scene.control.MenuItem;

WritableImage canvasSnapshot = null;

@Override
public void start(Stage primaryStage) {
    // ... existing code ...

    MenuItem undoItem = new MenuItem("Undo");
    undoItem.setOnAction(e -> {
        if (canvasSnapshot != null) {
            gc.drawImage(canvasSnapshot, 0, 0);
        }
    });
    editMenu.getItems().add(undoItem);

    canvas.setOnMousePressed(e -> {
        canvasSnapshot = canvas.snapshot(null, null);
        gc.beginPath();
    });
}
