# Eco-Friendly-Finder
An app that helps users find eco-friendly products, services, and businesses in their area, encouraging sustainability and reducing waste.
import React, { useState, useEffect } from 'react';
import { View, Text, StyleSheet, FlatList, TouchableOpacity } from 'react-native';
import axios from 'axios';

const EcoFriendlyFinder = () => {
  const [businesses, setBusinesses] = useState([]);

  useEffect(() => {
    const fetchBusinesses = async () => {
      try {
        const { data } = await axios.get('https://api.example.com/businesses');
        setBusinesses(data);
      } catch (error) {
        console.error(error);
      }
    };

    fetchBusinesses();
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Eco-Friendly Finder</Text>
      <FlatList
        data={businesses}
        keyExtractor={item => item.id}
        renderItem={({ item }) => (
          <TouchableOpacity style={styles.businessContainer} onPress={() => {}}>
            <Text style={styles.businessName}>{item.name}</Text>
            <Text style={styles.businessLocation}>{item.location}</Text>
          </TouchableOpacity>
        )}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  header: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 20,
  },
  businessContainer: {
    padding: 20,
    borderBottomWidth: 1,
    borderBottomColor: '#ccc',
  },
  businessName: {
    fontSize: 16,
    fontWeight: 'bold',
  },
  businessLocation: {
    fontSize: 14,
    color: '#888',
  },
});

export default EcoFriendlyFinder;
