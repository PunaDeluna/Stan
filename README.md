# Stan
Messenger
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

class TextMessenger {
    private Map<String, List<String>> conversations;

    public TextMessenger() {
        this.conversations = new HashMap<>();
    }

    public void sendMessage(String sender, String recipient, String message) {
        if (!conversations.containsKey(sender)) {
            conversations.put(sender, new ArrayList<>());
        }

        if (!conversations.containsKey(recipient)) {
            conversations.put(recipient, new ArrayList<>());
        }

        conversations.get(sender).add("You: " + message);
        conversations.get(recipient).add(sender + ": " + message);
    }

    public List<String> getConversation(String user) {
        return conversations.getOrDefault(user, new ArrayList<>());
    }

    public static void main(String[] args) {
        TextMessenger messenger = new TextMessenger();
        Scanner scanner = new Scanner(System.in);

        // Simulation of a conversation
        messenger.sendMessage("Alice", "Bob", "Hey, how's it going?");
        messenger.sendMessage("Bob", "Alice", "Hi! I'm good, thanks. How about you?");
        messenger.sendMessage("Alice", "Bob", "Not bad. What are you up to?");
        messenger.sendMessage("Bob", "Alice", "Just working on some coding. How about you?");

        // Display conversation
        System.out.println("Enter a username to view conversation:");
        String username = scanner.nextLine();

        List<String> conversation = messenger.getConversation(username);
        for (String message : conversation) {
            System.out.println(message);
        }

        scanner.close();
    }
}
