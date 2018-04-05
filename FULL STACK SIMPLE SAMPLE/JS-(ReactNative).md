## FULL STACK EXAMPLE  

    import React, { Component } from 'react';  
    import {  
        Text,  
        TextInput,  
        StyleSheet,  
        DatePickerIOS,  
        View,  
        Picker,  
        Button,  
        ScrollView,  
        KeyboardAvoidingView,  
        TouchableHighlight  
    } from 'react-native';  
    import * as exerciseServices from '../ExerciseServices';  
    import * as userServices from '../UserServices';  

    export default class Exercises extends Component {  

        state = {
            loading: false,
            exerciseTypeId: null,
            dateCompleted: new Date(),
            duration: null,
            description: null,
        }

        componentDidMount = () => {
        
            exerciseServices.getExerciseTypes().then(
                response => {

                    this.setState({ exerciseTypes: response.data });
                    const choices = this.state.exerciseTypes.map(item =>
                        <Picker.Item
                            key={item.Id}
                            label={item.Exercise}
                            value={item.Id} />)
                    this.setState({ choices: choices })
                },
                err => {
                    alert(err);
                }
            )
            
        }

        chosenDate = (dateChoice) => {
            this.setState({ dateCompleted: dateChoice })
        }

        validate = () => {
            let valid = this.state.exerciseTypeId && this.state.dateCompleted && this.state.duration > 0

            if (valid) {
                this.setState({ loading: true })

                const exerciseData = {
                    ExerciseTypeId: parseInt(this.state.exerciseTypeId),
                    DateCompleted: (this.state.dateCompleted).toISOString(),
                    Duration: parseInt(this.state.duration),
                    Description: this.state.description
                }

                return userServices.getCurrentUser().then(
                    response => {
                        exerciseData.userId = response.data;
                    },
                    err => {  
                        console.log(err)  
                        alert("Sorry we cannot complete your request, please try again");  
                    }
                ).then(
                    response => {
                        this.addExercise(exerciseData);
                    },
                    err => {   
                        console.log(err)  
                        alert("Sorry we cannot complete your request, please try again");  
                    }  
                )

            }

            if (!this.state.exerciseTypeId) {

                alert("Please choose a type an exercise");

            }

            return alert('Please enter valid data');
        }

        addExercise = (exerciseData) => {
            exerciseServices.createExercise(exerciseData).then(
                response => {
                    this.setState({
                        loading: false,
                        exerciseTypeId: null,
                        dateCompleted: new Date(),
                        duration: null,
                        description: null,
                    })
                    this.props.navigation.navigate('Home')
                },
                err => {
                    console.log(exerciseData)
                    alert('Unable to Complete Request')
                }
            );
        }

        
        render() {

            if (this.state.loading) {
                return (
                    <View style={styles.container}>
                        <View style={styles.content}>
                            <ActivityIndicator size="large" color="#78d3cf" />
                        </View>
                    </View>
                )
            }
            
            return (
                <KeyboardAvoidingView behavior="padding" style={styles.form}>
                    <Text style={styles.title}> Add Exercises </Text>
                    <ScrollView>
                        <View style={styles.content}>

                            <View style={styles.input}>
                                <Text style={styles.words}> Exercise Type </Text>
                                <Picker
                                    onValueChange={(itemValue, itemIndex) => this.setState({ exerciseTypeId: itemIndex })}
                                    selectedValue={this.state.exerciseTypeId}>
                                    <Picker.Item
                                        label='Please make a selection' value="0" />
                                    {this.state.choices}
                                </Picker>
                            </View>

                            <View style={styles.input}>
                                <Text style={styles.words}> Date Completed </Text>
                                <DatePickerIOS
                                    style={{ backgroundColor: '#fff' }}
                                    date={this.state.dateCompleted}
                                    onDateChange={this.chosenDate}
                                    mode="datetime"
                                />
                            </View>

                            <View style={styles.input}>
                                <Text style={styles.words}> Duration (in minutes) </Text>
                                <TextInput
                                    value={this.state.duration}
                                    onChangeText={value => this.setState({ duration: value })}
                                    style={styles.textBox}
                                    keyboardType="numeric"
                                />
                            </View>

                            <View style={styles.input}>
                                <Text style={styles.words}> Description </Text>
                                <TextInput
                                    style={styles.inputBox}
                                    multiline={true}
                                    numberOfLines={10}
                                    placeholder="Write a short description of your workout here"
                                    placeholderTextColor="#494949"
                                    selectionColor="#f27d7d"
                                    onChangeText={(value) => this.setState({ description: value })}
                                    value={this.state.description}
                                />
                            </View>

                            <View style={styles.buttonContainer}>
                                <TouchableHighlight style={styles.button} onPress={this.validate}>
                                    <Button color="#f27d7d" onPress={this.validate} title="Submit" />
                                </TouchableHighlight>
                            </View>
                        </View>
                    </ScrollView>
                </KeyboardAvoidingView>

            );
        }
    }

    const styles = StyleSheet.create({
        container: {
            display: 'flex',
            position: 'absolute',
            alignSelf: 'center',
            justifyContent: 'center',
            marginTop: 20,
            height: 850,
            width: 400,
            top: 0,
            left: 0,
            right: 0,
        },
        content: {
            flexDirection: "column",
            top: 8,
            marginBottom: 175,
            width: 300,
            alignSelf: 'center',
            marginLeft: 20,
            marginRight: 20,
        },
        buttonContainer: {
            flex: 1,
            height: 30,
            width: 'auto',
            alignItems: 'center',
            top: 30,
        },
        button: {
            borderColor: '#f27d7d',
            borderWidth: 3,
            backgroundColor: '#fff',
            alignItems: 'center',
            width: 250,
            height: 50,
        },
        words: {
            flexDirection: 'row',
            color: '#f27d7d',
            fontSize: 24,
            fontWeight: 'bold',
            marginBottom: 10,
        },
        title: {
            marginTop: 20,
            backgroundColor: '#494949',
            color: '#fff',
            fontSize: 24,
            top: 0,
            fontWeight: 'bold',
            textAlign: 'center',
        },
        input: {
            flex: 1,
            margin: 10,
        },
        inputBox: {
            borderTopWidth: 1,
            borderBottomWidth: 1,
            borderColor: "#494949",
            alignSelf: "center",
            color: '#494949',
        },
        textBox: {
            borderWidth: 1,
            borderColor: "#494949",
            height: 30,
            marginRight: 4,
        },
        form: {
            flex: 1,
            justifyContent: 'space-between',
        },
    });
