# BioZoomX MVP Specification

## ARCHITECTURE

The architectural design in the figure below is a simplified illustration of the flow of the components in the running of BioZoomX. The actual flow may be more complex.

1. The user's browser sends a request to the DNS server.
2. The DNS server resolves the domain name to an IP address.
3. The user's browser sends a request to the load balancer.
4. The load balancer distributes the request to one of the web servers.
5. The web server serves the static content of the BioZoomX website to the user's browser.
6. If the user requests the genome data for a simple organism, the web server will forward the request to the application server.
7. The application server will send a request to the API gateway.
8. The API gateway will route the request to the third party database API.
9. The third party database API will return the genome data to the API gateway.
10. The API gateway will return the genome data to the application server.
11. The application server will process the genome data and display it to the user's browser.
12. The user's browser may request the genome data again in the future. If so, the load balancer will cache the genome data in the cloud storage.
13. The next time the user requests the genome data, the load balancer will serve the genome data from the cloud storage.
14. The CDN will cache the static content of the BioZoomX website in multiple locations around the world.
15. If the user is located close to a CDN node, the CDN will serve the static content of the BioZoomX website to the user's browser.

img link coming soon

# APIs and Methods

## API Routes for Web Client Communication with Application Server:

- `/api/genome_data`
  - **GET:** Returns genome data for a specified organism.
  - **Parameters:** Organism ID or name.

- `/api/user_data`
  - **GET:** Returns user-specific data.
  - **Parameters:** User ID, authentication token.

- `/api/visualization`
  - **POST:** Returns processed data for visualization.
  - **Parameters:** User ID, selected data range.

## API Endpoints for External Clients:

### BioZoomX.getGenomeData(organism)

- **Description:** Allows external clients to retrieve genome data for a specific organism.
- **Parameters:** Organism ID or name.
- **Returns:** Genome data in a structured format.

### BioZoomX.processData(data)

- **Description:** Provides external clients with the ability to process raw genetic data.
- **Parameters:** Raw data in a specific format.
- **Returns:** Processed data for visualization.

### BioZoomX.getUserInsights(userId)

- **Description:** Enables external clients to access insights derived from user interactions.
- **Parameters:** User ID.
- **Returns:** Insights and analytics related to user interactions.

## Third-Party APIs:

### NCBI Entrez API

- **Description:** Provides access to genetic and genomic data from the National Center for Biotechnology Information (NCBI).
- **Usage:** Retrieve genetic sequences, annotations, and related data for different organisms.

### Ensembl REST API

- **Description:** Offers programmatic access to genome annotations and related data.
- **Usage:** Retrieve gene information, sequence data, and functional annotations.

### Cloud Storage API (e.g., Amazon S3)

- **Description:** Allows for storage and retrieval of large datasets, including genetic data files.
- **Usage:** Store and retrieve data files for processing and analysis.

# Data Model

## User

- **Fields:** User ID, Username, Email, Password, User Preferences
- **Relationships:** One-to-Many with User Interactions

## GenomeData

- **Fields:** Organism ID, Genome Sequence, Annotations, Genetic Data
- **Relationships:** One-to-Many with User Interactions

## UserInteractions

- **Fields:** Interaction ID, User ID, Action Type, Timestamp
- **Relationships:** Many-to-One with User and GenomeData

## ProcessedData

- **Fields:** Data ID, Processed Result, Visualization Details
- **Relationships:** One-to-One with GenomeData

## ThirdPartyData

- **Fields:** Data ID, Source, Data Content
- **Relationships:** One-to-Many with GenomeData

# User Stories

- As a biologist, I want to search for genome data by specifying the organism name or ID so that I can retrieve relevant genetic information for my research.
- As a user, I want to visualize genetic sequence annotations in a graphical format, allowing me to analyze the structure and function of genes.
- As a researcher, I want to explore processed genetic data visually with interactive zoom and slider controls, enabling a detailed examination of specific genomic regions.
- As a user, I want to save and revisit visualizations I've created, so that I can compare different datasets and share insights with my colleagues.
- As a developer, I want to ensure that user interactions with the application are fast and responsive, enabling a seamless experience for data exploration.



