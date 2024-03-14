package com.example.javafx;

import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.image.Image;
import javafx.scene.layout.Pane;
import javafx.scene.image.ImageView;
import javafx.scene.layout.BorderPane;
import javafx.scene.layout.GridPane;
import javafx.scene.layout.HBox;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class ImageGalleryApplication extends Application {

    private final String[] imageUrls = {
            "red.jpg",
            "white.jpg",
            "pexels.jpg",
            "Cars.jpg",
            "Black.jpg"
    };
    private BorderPane root = new BorderPane();
    private GridPane imageGrid = new GridPane();
    private ImageView currentImageView = new ImageView();
    private int currentImageIndex = 0;

    @Override
    public void start(Stage primaryStage) {
        displayImages();

        Button previousButton = new Button("Previous");
        previousButton.setOnAction(e -> showPreviousImage());

        Button nextButton = new Button("Next");
        nextButton.setOnAction(e -> showNextImage());

        Button thumbnailsButton = new Button("Thumbnails");
        thumbnailsButton.setOnAction(e -> displayImages());

        HBox navigationBox = new HBox(previousButton, nextButton, thumbnailsButton);
        navigationBox.setSpacing(10);
        root.setBottom(navigationBox);

        VBox imageBox = new VBox();
        imageBox.getChildren().add(currentImageView);
        imageBox.setPadding(new Insets(20));
        imageBox.setSpacing(10);
        root.setCenter(imageBox);

        Scene scene = new Scene(root, 1000, 800);

        // Ensure that the CSS file path is correct
        scene.getStylesheets().add(getClass().getResource("ImageGallery.css").toExternalForm());

        primaryStage.setScene(scene);
        primaryStage.setTitle("Image Gallery");
        primaryStage.show();
    }

    private void displayImages() {
        // Clear previous images
        imageGrid.getChildren().clear();

        // Populate grid with thumbnail images
        for (int i = 0; i < imageUrls.length; i++) {
            Image thumbnail = loadImage(imageUrls[i]);
            if (thumbnail != null) {
                ImageView thumbnailView = new ImageView(thumbnail);
                thumbnailView.setFitWidth(100);
                thumbnailView.setFitHeight(100);
                int index = i; // Needed for lambda expression
                thumbnailView.setOnMouseClicked(e -> showFullImage(imageUrls[index]));
                imageGrid.add(thumbnailView, i % 3, i / 3);
            }
        }

        root.setCenter(imageGrid);
    }

    private Image loadImage(String imageUrl) {
        try {
            return new Image(getClass().getResourceAsStream(imageUrl));
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return null;
        }
    }

    private void showFullImage(String imageUrl) {
        Image fullImage = loadImage(imageUrl);
        if (fullImage != null) {
            currentImageView.setImage(fullImage);
        }
    }

    private void showNextImage() {
        currentImageIndex = (currentImageIndex + 1) % imageUrls.length;
        showFullImage(imageUrls[currentImageIndex]);
    }

    private void showPreviousImage() {
        currentImageIndex = (currentImageIndex - 1 + imageUrls.length) % imageUrls.length;
        showFullImage(imageUrls[currentImageIndex]);
    }

    public static void main(String[] args) {
        launch(args);
    }
}
