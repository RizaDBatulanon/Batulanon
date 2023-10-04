import React, { useState, useEffect } from 'react';
import { StyleSheet, Text, View, TextInput, TouchableOpacity, FlatList, Image } from 'react-native';

export default function App() {
  const [messages, setMessages] = useState([]);
  const [inputMessage, setInputMessage] = useState('');

  useEffect(() => {
    // Simulated initial messages when the component mounts
    const initialMessages = [
      {
        id: '1',
        text: 'Hi gaw',
        user: {
          name: 'Gaw Gab',
          avatarUrl: 'https://th.bing.com/th/id/OIP.iYTOaXdMwbOKU-KoZ_sHxQHaFj?w=246&h=184&c=7&r=0&o=5&pid=1.7',
        },
      },
      {
        id: '2',
        text: 'Good Morning kuya',
        user: {
          name: 'Jesreel',
          avatarUrl: 'https://wallpapertag.com/wallpaper/full/e/3/b/962077-love-wallpapers-images-1242x2208-hd-1080p.jpg',
        },
      },
  {
      id: '3',
        text: 'Hi hon , kumusta',
        user: {
          name: 'Honey Irene',
          avatarUrl: 'https://th.bing.com/th?id=OIP.KC7Bn6be0WJb7YK9PvxvWAHaLH&w=204&h=306&c=8&rs=1&qlt=90&o=6&pid=3.1&rm=2',
        },
      },
    {
      id: '4',
        text: 'DATABAL',
        user: {
          name: '8080',
          avatarUrl: 'https://th.bing.com/th/id/OIP.5SjKih2sQZ_ysAcRIOzJhgHaEo?w=357&h=184&c=7&r=0&o=5&pid=1.7',
        },
      },
      // Add more initial messages as needed
    ];

    setMessages(initialMessages);
  }, []);

  const handleSendMessage = () => {
    if (inputMessage.trim() !== '') {
      const newMessage = {
        id: Date.now().toString(),
        text: inputMessage,
        user: {
          name: 'Jesreel', // You can replace this with the authenticated user's name
          avatarUrl: '', // You can replace this with the authenticated user's avatar URL
        },
      };

      setMessages([...messages, newMessage]);
      setInputMessage('');
    }
  };

  return (
    <View style={styles.container}>
      <View style={styles.header}>
        <Text style={styles.headerText}>Messages</Text>
      </View>
      <FlatList
        data={messages}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <View style={styles.messageContainer}>
            <Image source={{ uri: item.user.avatarUrl }} style={styles.avatar} />
            <View style={styles.messageContent}>
              <Text style={styles.userName}>{item.user.name}</Text>
              <Text style={styles.messageText}>{item.text}</Text>
            </View>
          </View>
        )}
      />
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          placeholder="Type your message..."
          value={inputMessage}
          onChangeText={(text) => setInputMessage(text)}
        />
        <TouchableOpacity style={styles.sendButton} onPress={handleSendMessage}>
          <Text style={styles.sendButtonText}>Send</Text>
        </TouchableOpacity>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
  },
  header: {
    paddingTop: 40,
    paddingBottom: 10,
    backgroundColor: '#1DA1F2',
    alignItems: 'center',
  },
  headerText: {
    fontSize: 20,
    fontWeight: 'bold',
    color: '#fff',
  },
  messageContainer: {
    flexDirection: 'row',
    alignItems: 'center',
    padding: 10,
    borderBottomWidth: 1,
    borderBottomColor: '#ccc',
  },
  avatar: {
    width: 50,
    height: 50,
    borderRadius: 25,
    marginRight: 10,
  },
  messageContent: {
    flex: 1,
  },
  userName: {
    fontWeight: 'bold',
    fontSize: 16,
  },
  messageText: {
    fontSize: 16,
  },
  inputContainer: {
    flexDirection: 'row',
    alignItems: 'center',
    borderTopWidth: 1,
    borderTopColor: '#ccc',
    paddingHorizontal: 16,
  },
  input: {
    flex: 1,
    height: 40,
    borderWidth: 1,
    borderColor: '#ccc',
    borderRadius: 20,
    paddingHorizontal: 16,
  },
  sendButton: {
    marginLeft: 10,
    paddingVertical: 10,
  },
  sendButtonText: {
    color: '#1DA1F2',
    fontWeight: 'bold',
  },
});

