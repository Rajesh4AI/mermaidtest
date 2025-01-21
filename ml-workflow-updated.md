flowchart TB
    Start([Start]) --> LoadData[/"Load Data from CSV
    load_data()"/]
    
    subgraph Preprocessing["Preprocessing Section"]
        LoadData --> Preprocess["Preprocess Data
        preprocess_data()"]
        Preprocess -->|"Returns"| DataSplit["X_train, X_test,
        y_train, y_test, scaler"]
        DataSplit --> PrintShapes["Print Dataset Shapes
        print_shapes()"]
    end
    
    subgraph MainPipeline["Evaluate and Tune Pipeline"]
        PrintShapes --> EvalTune["evaluate_and_tune()"]
        
        subgraph ModelFlow["Model Building & Evaluation Flow"]
            BuildModel["Build Model
            build_model()"] --> CrossValTune["run_cross_validation_and_tuning()"]
            
            subgraph CVTuning["Cross-Validation & Tuning"]
                CrossVal["Cross Validation
                cross_validate_model()"] --> TuneModel["Hyperparameter Tuning
                tune_model()"]
            end
            
            CrossValTune --> TrainModel["Train Model
            train_model()"]
            TrainModel --> EvalModel["Evaluate Model
            evaluate_model()"]
        end
        
        EvalTune --> Results["Output Results:
        - Accuracy Score
        - Classification Report"]
    end
    
    Results --> End([End])
    
    classDef process fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef section fill:#fff3e0,stroke:#ff6f00,stroke-width:2px
    classDef subsection fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    
    class LoadData,Preprocess,PrintShapes,BuildModel,CrossVal,TuneModel,TrainModel,EvalModel process
    class Preprocessing,MainPipeline section
    class ModelFlow,CVTuning subsection
