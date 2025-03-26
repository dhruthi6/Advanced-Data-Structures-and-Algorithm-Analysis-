import java.io.*;
import java.util.*;

class AVLNode {
    int key;
    AVLNode left, right;
    int height;

    AVLNode(int key) {
        this.key = key;
        height = 0;
        left = right = null;
    }
}

public class AVLTree {

    public static int height(AVLNode node) {
        return node == null ? -1 : node.height;
    }

    public static AVLNode rotateWithLeftChild(AVLNode k2) {
        AVLNode k1 = k2.left;
        k2.left = k1.right;
        k1.right = k2;
        k2.height = Math.max(height(k2.left), height(k2.right)) + 1;
        k1.height = Math.max(height(k1.left), k2.height) + 1;
        return k1;
    }

    public static AVLNode rotateWithRightChild(AVLNode k1) {
        AVLNode k2 = k1.right;
        k1.right = k2.left;
        k2.left = k1;
        k1.height = Math.max(height(k1.left), height(k1.right)) + 1;
        k2.height = Math.max(height(k2.right), k1.height) + 1;
        return k2;
    }

    public static AVLNode doubleWithLeftChild(AVLNode k3) {
        k3.left = rotateWithRightChild(k3.left);
        return rotateWithLeftChild(k3);
    }

    public static AVLNode doubleWithRightChild(AVLNode k1) {
        k1.right = rotateWithLeftChild(k1.right);
        return rotateWithRightChild(k1);
    }

    public static AVLNode insert(int key, AVLNode node) {
        if (node == null)
            return new AVLNode(key);

        if (key < node.key) {
            node.left = insert(key, node.left);
            if (height(node.left) - height(node.right) == 2)
                node = (key < node.left.key) ? rotateWithLeftChild(node) : doubleWithLeftChild(node);
        } else if (key > node.key) {
            node.right = insert(key, node.right);
            if (height(node.right) - height(node.left) == 2)
                node = (key > node.right.key) ? rotateWithRightChild(node) : doubleWithRightChild(node);
        }
        node.height = Math.max(height(node.left), height(node.right)) + 1;
        return node;
    }

    public static AVLNode findMin(AVLNode node) {
        return (node == null || node.left == null) ? node : findMin(node.left);
    }

    public static AVLNode delete(int key, AVLNode node) {
        if (node == null) return null;

        if (key < node.key) node.left = delete(key, node.left);
        else if (key > node.key) node.right = delete(key, node.right);
        else {
            if (node.left != null && node.right != null) {
                AVLNode minNode = findMin(node.right);
                node.key = minNode.key;
                node.right = delete(minNode.key, node.right);
            } else node = (node.left != null) ? node.left : node.right;
        }

        if (node != null) {
            node.height = Math.max(height(node.left), height(node.right)) + 1;
            if (height(node.left) - height(node.right) == 2)
                node = (height(node.left.left) >= height(node.left.right)) ? rotateWithLeftChild(node) : doubleWithLeftChild(node);
            else if (height(node.right) - height(node.left) == 2)
                node = (height(node.right.right) >= height(node.right.left)) ? rotateWithRightChild(node) : doubleWithRightChild(node);
        }
        return node;
    }

    public static void inOrder(AVLNode node, BufferedWriter writer) throws IOException {
        if (node != null) {
            inOrder(node.left, writer);
            writer.write(node.key + " ");
            inOrder(node.right, writer);
        }
    }

    public static void main(String[] args) throws IOException {
        AVLNode root = null;
        Scanner scanner = new Scanner(new File("input.txt"));
        while (scanner.hasNextInt()) {
            root = insert(scanner.nextInt(), root);
        }
        scanner.close();

        root = delete(13, root);

        BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"));
        inOrder(root, writer);
        writer.close();
        System.out.println("In-order traversal written to output.txt");
    }
}
